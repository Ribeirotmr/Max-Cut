
# QAOA para o MaxCut

## 📖 Introdução

> **Definição do problema MaxCut**: "Dado um grafo G = (V,E) não direcionado onde cada aresta de E é ponderada com um número inteiro, o problema de corte máximo (Max-Cut) consiste em particionar os vértices de V em dois subconjuntos disjuntos de modo a maximizar o peso total das arestas entre os dois subconjuntos."  
> *(Benlic & Jin-Kao, 2013. Tradução nossa.)*

### 🔗 Referências:
- [Hidary2021](https://drive.google.com/file/d/1J8Nv8ufZ13RcRFVveyyzfODukO-eWYDV/view?usp=drive_link) — Jack D. Hidary: *Quantum Computing: An Applied Approach* - 2nd edition. Springer, 2021: pp.156-159.
- Una Benlic, Jin-Kao (2013): *Breakout Local Search for the Max-Cut problem*. Engineering Applications of Artificial Intelligence, Volume 26, Issue 3, March 2013, Pages 1162-1173. [DOI](https://www.sciencedirect.com/science/article/abs/pii/S0952197612002175)

---

## 🎯 MaxCut e sua Quantização

Considere um grafo não-orientado com pesos:

$$
\\mathcal{G} = (V,E,W)
$$

- Conjunto de vértices, onde $n_V \\in \\mathbb{N}$ é o número de vértices:

$$
V = \\left\\{ i;\\ i = 0, \\dots, n_V-1 \\right\\}
$$

- Conjunto de arestas:

$$
E \\subset V \\times V
$$

- Conjunto de pesos:

$$
W = \\left\\{ w_{ij} \\in \\mathbb{R};\\ i,j \\in V\\right\\}
$$

Com a condição:

$$
w_{ij} = 0,\\ \\forall i,j \\in V\\ /\\ (i,j) \\notin E
$$

---

> **Problema MaxCut:**  
O problema MaxCut para o grafo $\\mathcal{G}$ consiste em determinar uma partição do conjunto de vértices $V$ em dois subconjuntos, digamos $V_0$ e $V_1$, de modo a maximizar a soma dos pesos associados às arestas que têm um vértice em $V_0$ e outro vértice em $V_1$.

---

Para representar matematicamente o problema, associamos cada partição $\\{V_0, V_1\\}$ a um vetor binário:

$$
\\mathbf{z} = (z_0, z_1, \\dots, z_{n_V-1}) \\in \\{0, 1\\}^{n_V}
$$

Com:

$$
z_k =
\\begin{cases}
0, & \\text{se } v_k \\in V_0\\\\
1, & \\text{se } v_k \\in V_1
\\end{cases}
$$

---

A função custo do problema é expressa como:

$$
C(\\mathbf{z}) = \\frac{1}{2}\\sum_{i,j\\in V} w_{ij}\\left(1- (-1)^{z_i}(-1)^{z_j}\\right)
$$

Portanto, o problema MaxCut se traduz como:

$$
\\underset{\\mathbf{z} \\in \\{0, 1\\}^{n_V}}{\\arg\\max} C(\\mathbf{z})
$$

---

## 🧠 Quantização

Definimos um espaço de qubits associado ao problema e um hamiltoniano correspondente:

- Espaço de Hilbert:

$$
\\mathcal{H} = \\mathcal{H}_1^{\\otimes n_V}
$$

- Hamiltoniano custo:

$$
H_C = \\frac{1}{2}\\sum_{i,j \\in V} w_{ij} (I - Z_iZ_j)
$$

Onde $Z_k$ é o operador de Pauli-Z aplicado no $k$-ésimo qubit:

$$
Z_k |z_{n_V - 1}\\dots z_1z_0 \\rangle = (-1)^{j_k} |z_{n_V - 1}\\dots z_1z_0 \\rangle
$$

---

**Observação:**  
$H_C$ é um operador diagonal na base computacional, com autovalores correspondendo às imagens da função custo:

$$
H_C |z_{n_V - 1} \\dots z_1 z_0 \\rangle = C(\\mathbf{z}) |z_{n_V - 1} \\dots z_1 z_0 \\rangle
$$

---

<font color="red"><b>Resolver o MaxCut corresponde a determinar o autoestado associado ao maior autovalor de $H_C$.</b></font>

---

## 🔗 Licença

Este projeto está licenciado sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

---

## 🚀 Sobre

Este README faz parte do projeto de estudo sobre QAOA (Quantum Approximate Optimization Algorithm) aplicado ao problema MaxCut.

---

