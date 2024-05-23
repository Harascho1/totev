# totev
void GraphAsListsInt::createDepthOrderTraversalGraph(int data, GraphAsListsInt& graph) {

	LinkedNodeInt* ptr = findNode(data);
	if (ptr == nullptr)
		return;

	setStatusForAllNodes(1);

	StackAsArrayLinkedNodeInt stack(nodeNum);
	stack.push(ptr);
	ptr->status = 2;
	graph.insertNode(ptr->node);
	while (!stack.isEmpty()) {
		ptr = stack.pop();
		ptr->status = 3;
		LinkedEdgeInt* pEdge = ptr->adj;
		while (pEdge != nullptr) {
			if (pEdge->dest->status == 1) {
				stack.push(pEdge->dest);
				pEdge->dest->status = 2;
				graph.insertNode(pEdge->dest->node);
				graph.insertEdge(ptr->node, pEdge->dest->node);
			}
			pEdge = pEdge->link;
		}
	}
}
