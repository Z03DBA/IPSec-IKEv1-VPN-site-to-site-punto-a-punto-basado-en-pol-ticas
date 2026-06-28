# 🔒 Práctica 1: VPN Site-to-Site Basada en Políticas (IPsec IKEv1)

Este repositorio contiene la configuración, topología y documentación técnica para la implementación de una Red Privada Virtual (VPN) Punto a Punto basada en políticas, utilizando routers Cisco IOS en el simulador GNS3.

## 👥 Datos del Estudiante
* **Nombre:** Zoe Daniela Bobonagua Acevedo
* **Matrícula:** 2024-0927
* **Carrera:** Tecnólogo en Seguridad Informática (ITLA)
* **Asignación:** Práctica 1 (P1)

---

## 🗺️ Esquema de la Topología
La topología implementada cuenta con una arquitectura lineal compuesta por un proveedor de servicios (ISP) interconectando dos sucursales (Peer A y Peer B). El direccionamiento lógico se derivó de forma estricta utilizando la dirección de red base asignada por matrícula: `192.8.39.0`.

* **Router 1 (ISP Central):** * `Gi1/0` (Hacia R2): `192.8.39.2/30`
  * `Gi2/0` (Hacia R3): `192.8.39.6/30`
* **Router 2 (Peer A - Izquierda):**
  * `Gi1/0` (WAN): `192.8.39.1/30`
  * `Gi2/0` (LAN A): `192.8.39.65/26`
  * **PC1 (Host LAN A):** `192.8.39.66/26` (Gateway: `192.8.39.65`)
* **Router 3 (Peer B - Derecha):**
  * `Gi1/0` (WAN): `192.8.39.5/30`
  * `Gi2/0` (LAN B): `192.8.39.129/26`
  * **PC2 (Host LAN B):** `192.8.39.130/26` (Gateway: `192.8.39.129`)

---

## 🛡️ Parámetros Criptográficos Aplicados (Fase 1 y Fase 2)
* **Cifrado (Fase 1):** AES-256
* **Integridad (Hash):** SHA-256
* **Autenticación:** Pre-Shared Key (`cisco123`)
* **Grupo Diffie-Hellman:** Group 14 (2048 bits)
* **Transform-Set (Fase 2):** `esp-aes 256 esp-sha256-hmac`
* **Modo de Operación:** Tunnel Mode

---

## 🚀 Comandos de Verificación Clave
Para demostrar el correcto funcionamiento en el video adjunto, ejecute los siguientes comandos en las consolas de los equipos:

```bash
# Verificar que la Fase 1 negoció con éxito (Estado: QM_IDLE)
show crypto isakmp sa

# Verificar la Fase 2 y comprobar el incremento de paquetes encriptados/desencriptados
show crypto ipsec sa

# Comprobar conectividad IP asignada a las interfaces
show ip interface brief
