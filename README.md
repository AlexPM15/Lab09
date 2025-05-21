# Lab09
class NodoArbol:
    def __init__(self, valor):
        self.valor = valor
        self.hijos = []  # Lista de hijos, que son otros NodoArbol


    def agregar_hijo(self, nuevo_hijo):
        """Agrega un hijo al nodo actual"""
        self.hijos.append(nuevo_hijo)


    def eliminar_hijo_por_valor(self, valor_hijo):
        """Elimina el hijo con el valor indicado"""
        for i, hijo in enumerate(self.hijos):
            if hijo.valor == valor_hijo:
                del self.hijos[i]
                return True
        return False


    def buscar(self, valor):
        """Busca un nodo por valor usando recorrido DFS"""
        if self.valor == valor:
            return self
        for hijo in self.hijos:
            resultado = hijo.buscar(valor)
            if resultado:
                return resultado
        return None


    def imprimir(self, nivel=0):
        """Imprime el árbol con indentación para visualizar estructura"""
        print("  " * nivel + f"- {self.valor}")
        for hijo in self.hijos:
            hijo.imprimir(nivel + 1)
    def contar_nodos(self):
            total = 1

            for hijo in self.hijos:
                total += hijo.contar_nodos()      
            return total
    def contar_hojas(self):
        if not self.hijos:
            return 1
        total_hojas = 0
        for hijo in self.hijos:
            total_hojas += hijo.contar_hojas()
            
        return total_hojas
    def existe_valor(self, valor):
        if self.valor == valor:
            return True
        
        # Buscar en cada hijo
        for hijo in self.hijos:
            if hijo.existe_valor(valor):
                return True
            return False
# Crear raíz
raiz = NodoArbol("A")

# Agregar hijos a la raíz
raiz.agregar_hijo(NodoArbol("B"))
raiz.agregar_hijo(NodoArbol("C"))
raiz.agregar_hijo(NodoArbol("D"))

# Agregar nietos al nodo B
nodo_b = raiz.buscar("B")
nodo_b.agregar_hijo(NodoArbol("E"))
nodo_b.agregar_hijo(NodoArbol("F"))

# Mostrar árbol
print("Árbol antes de eliminar:")
raiz.imprimir()

# Eliminar hijo "F" de "B"
resultado = nodo_b.eliminar_hijo_por_valor("F")
print(f"\nEliminación exitosa: {resultado}")
print("Árbol después de eliminar 'F':")
raiz.imprimir()

# Agregar hijos al nodo F para probar la restricción de eliminación
nodo_b = raiz.buscar("B")
nodo_f = NodoArbol("F")
nodo_f.agregar_hijo(NodoArbol("G"))
nodo_b.agregar_hijo(nodo_f)

print("\nÁrbol con F que tiene hijo G:")
raiz.imprimir()

# Intentar eliminar F (ahora no debería permitirlo)
resultado = nodo_b.eliminar_hijo_por_valor("F")
print(f"\nEliminación exitosa de F con hijos: {resultado}")
print("Árbol después de intentar eliminar 'F' con hijos:")
raiz.imprimir()

# Probar los desafíos implementados
print("\n----- DESAFÍOS -----")
print(f"1. Total de nodos en el árbol: {raiz.contar_nodos()}")
print(f"2. Total de hojas en el árbol: {raiz.contar_hojas()}")
print(f"3. ¿Existe el valor 'E' en el árbol?: {raiz.existe_valor('E')}")
print(f"3. ¿Existe el valor 'Z' en el árbol?: {raiz.existe_valor('Z')}")
print(f"4. Lista de todos los valores del árbol: {raiz.listar_valores()}")
