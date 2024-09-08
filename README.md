# BFS-
this is a breath first search program.

#include <stdio.h>
#include <stdlib.h>

#define MAX 100

int queue[MAX], front = -1, rear = -1;
int visited[MAX] = {0}; // To mark visited nodes
int adjMatrix[MAX][MAX]; // Graph adjacency matrix
int n; // Number of nodes

// Enqueue function to add element to queue
void enqueue(int item) {
    if (rear == MAX - 1) return; // Queue overflow
    if (front == -1) front = 0;
    queue[++rear] = item;
}

// Dequeue function to remove element from queue
int dequeue() {
    if (front == -1 || front > rear) return -1; // Queue empty
    return queue[front++];
}

// BFS function
void bfs(int startNode) {
    enqueue(startNode);
    visited[startNode] = 1;

    while (front <= rear) {
        int currentNode = dequeue();
        printf("%d ", currentNode);

        for (int i = 0; i < n; i++) {
            if (adjMatrix[currentNode][i] == 1 && !visited[i]) {
                enqueue(i);
                visited[i] = 1;
            }
        }
    }
}

int main() {
    int edges, u, v, start;

    printf("Enter the number of nodes: ");
    scanf("%d", &n);
    
    printf("Enter the number of edges: ");
    scanf("%d", &edges);

    // Input graph connections (edges)
    for (int i = 0; i < edges; i++) {
        printf("Enter edge (u v): ");
        scanf("%d %d", &u, &v);
        adjMatrix[u][v] = 1; // Assuming directed graph
        adjMatrix[v][u] = 1; // For undirected graph
    }

    printf("Enter the start node for BFS: ");
    scanf("%d", &start);

    printf("BFS Traversal: ");
    bfs(start);

    return 0;
}

