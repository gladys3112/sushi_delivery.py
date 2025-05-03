# sushi_delivery.py
menu de sushi 

rolls = {
    "1": {"nombre": "Pikachu Roll", "precio": 4500},
    "2": {"nombre": "Otaku Roll", "precio": 5000},
    "3": {"nombre": "Pulpo Venenoso Roll", "precio": 5200},
    "4": {"nombre": "Anguila Eléctrica Roll", "precio": 4800}
}

    print("\n********* MENÚ DE SUSHI *********")
    for clave, datos in rolls.items():
        print(f"{clave}. {datos['nombre']} - ${datos['precio']}")
    print("5. Finalizar pedido")

def mostrar_resumen(pedido, descuento_aplicado):
    total_productos = sum(pedido.values())
    subtotal = sum(pedido[clave] * rolls[clave]["precio"] for clave in rolls)
    descuento = int(subtotal * 0.10) if descuento_aplicado else 0
    total = subtotal - descuento

    print("\n********* DETALLE DEL PEDIDO *********")
    print(f"TOTAL PRODUCTOS: {total_productos}")
    for clave, datos in rolls.items():
        print(f"{datos['nombre']}: {pedido[clave]}")
    print("**************************************")
    print(f"Subtotal por pagar: ${subtotal}")
    print(f"Descuento por código: ${descuento}")
    print(f"TOTAL: ${total}")
    print("**************************************")

def pedir_codigo_descuento():
    while True:
        codigo = input("¿Tienes un código de descuento? (escribe el código o 'X' para omitir): ").lower()
        if codigo == "soyotaku":
            print("¡Código válido! Se aplicará un 10% de descuento.")
            return True
        elif codigo == "x":
            return False
        else:
            print("Código no válido. Inténtalo nuevamente o escribe 'X' para volver al menú.")

def hacer_pedido():
    pedido = {clave: 0 for clave in rolls}

    while True:
        mostrar_menu()
        opcion = input("Selecciona una opción (1-5): ")
        if opcion in rolls:
            pedido[opcion] += 1
            print(f"Agregado: {rolls[opcion]['nombre']}")
        elif opcion == "5":
            break
        else:
            print("Opción inválida. Intenta nuevamente.")

    if sum(pedido.values()) == 0:
        print("No se han agregado productos al pedido.")
        return

    descuento_aplicado = pedir_codigo_descuento()
    mostrar_resumen(pedido, descuento_aplicado)

def main():
    while True:
        hacer_pedido()
        continuar = input("\n¿Deseas realizar otro pedido? (s/n): ").lower()
        if continuar != "s":
            print("Gracias por tu compra. ¡Hasta pronto!")
            break

if __name__ == "__main__":
    main()
