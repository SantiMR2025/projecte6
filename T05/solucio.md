# Guia Tècnica de Seguretat

Xifratge de Dades i Verificació d’Integritat  
Projecte Nexus

## 1. Objectiu de la Guia

Aquesta guia descriu de manera tècnica i formal els procediments realitzats per garantir la confidencialitat i integritat de la informació acadèmica del Projecte Nexus mitjançant l’ús de:

*   Xifratge simètric amb VeraCrypt
*   Funcions hash SHA‑256 per a control d’integritat

El document està orientat a entorns Windows 11 (VirtualBox).

***

## 2. Fonaments Teòrics

### 2.1 Xifratge vs. Hashing

El xifratge converteix informació llegible en dades inintel·ligibles mitjançant una clau, i és reversible. Garanteix la confidencialitat del contingut.  
Una funció hash genera una empremta digital única i irreversible del fitxer, utilitzada per comprovar-ne la integritat.  
Un canvi mínim al document produeix un hash completament diferent.

***

## 3. Tasca 1

Protecció de dades en repos amb VeraCrypt

### 3.1 Configuració del volum xifrat

*   instalacio de VeraCrypt
*   Tipus de volum: Standard File Container
*   Tamany: 100 MB
*   Algorisme de xifratge: AES‑256
*   Algorisme de hash: SHA‑512
*   Nom del volum: `exam_nexus.vc`

**Captura requerida:** Configuració del volum amb AES‑256  

![img](img/0001.png)
![img](img/0002.png)
![img](img/0003.png)
![img](img/0004.png)
![img](img/0016.png)
![img](img/0007.png)
![img](img/0008.png)
![img](img/0011.png)
![img](img/0012.png)
![img](img/0013.png)
![img](img/0015.png)
![img](img/0014.png)


***

### 3.2 Muntatge del volum i creació de l'examen

A la unitat muntada (per exemple X:), s’ha creat:

`EXAMEN_FINAL_SEGURETAT.txt`

Contingut: preguntes d'examen de prova.

![img](img/0017.png)

***

### 3.3 Verificació de la confidencialitat

1.  Amb la unitat muntada, el fitxer pot ser obert.
2.  En desmuntar el volum, la unitat desapareix i el fitxer deixa de ser accessible.

![img](img/001.png)

***

## 4. Tasca 2

Verificació d’integritat amb SHA‑256 (CertUtil)

### 4.1 Fitxer original

Nom: `nota_final_curs.txt`  
Contingut:

    L'alumne ha aprovat amb un 5

Comanda utilitzada (Windows CMD):

    CertUtil -hashfile "ruta\nota_final_curs.txt" SHA256

![img](img/0019.png)
![img](img/0018.png)

***

### 4.2 Fitxer modificat

Nou contingut:

    L'alumne ha aprovat amb un 9

Mateix comandament SHA‑256 executat novament.

![img](img/0020.png)
![img](img/0021.png)

***

### 4.3 Resultats

La modificació d’un únic caràcter genera un hash completament diferent, demostrant:

*   la propietat d’avalança
*   la capacitat de detectar manipulacions
*   la robustesa de SHA‑256 per a control d’integritat

***

## 5. Conclusions i Recomanacions

1.  **Protecció de dades sensibles:**  
    L’ús de volums xifrats amb AES‑256 evita filtracions d’exàmens i dades acadèmiques en dispositius portàtils.

2.  **Contrasenyes robustes:**  
    Recomanable utilitzar gestors de contrasenyes i NO reutilitzar credencials.

3.  **Verificació d’integritat amb hashing:**  
    Imprescindible per assegurar que actes de notes, programari i contractes no han estat alterats.

4.  **Combinació necessària de tècniques:**  
    El xifratge protegeix la confidencialitat; el hashing protegeix la integritat. Ambdues tècniques són complementàries i essencials per la seguretat global.

Vols que afegeixi una portada formal, un índex automàtic o un format més acadèmic?
