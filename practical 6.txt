n = int(input("Enter number of departments: "))

names = []

for i in range(n):
    name = input("Enter name of department: ")
    names.append(name)

print("\nEnter the distance matrix:")
print("Enter 0 if there is no direct connection.")

graph = []

for i in range(n):
    row = []
    for j in range(n):
        d = int(input("Distance from " + names[i] + " to " + names[j] + ": "))
        row.append(d)
    graph.append(row)

def find(parent, x):
    while parent[x] != x:
        x = parent[x]
    return x

edges = []

for i in range(n):
    for j in range(i + 1, n):
        if graph[i][j] != 0:
            edges.append((graph[i][j], i, j))

edges.sort()

parent = list(range(n))
mst = []
total = 0

for dist, u, v in edges:
    root_u = find(parent, u)
    root_v = find(parent, v)

    if root_u != root_v:
        parent[root_u] = root_v
        mst.append((u, v, dist))
        total += dist

        if len(mst) == n - 1:
            break

print("\nMinimum Spanning Tree using Kruskal's Algorithm:")

for u, v, d in mst:
    print(names[u], "---", names[v], ":", d, "m")

print("Total distance =", total, "m")

if len(mst) < n - 1:
    print("Graph is not fully connected.")