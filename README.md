# T1. 2ona Convocatòria: Recull d’activitats

## 1. En el següent llistat de tecnologies de la comunicació es fan servir una o diverses tècniques d’encriptació vistes a classe (hashing, simètrica o asimètrica). Cerca i determina quina o quines fan servir. Explica en quin punt les fa servir i per què aquesta tècnica.
**TLS/HTTPS**
- Asimètrica: durant l’establiment de connexió (handshake), s’utilitza per intercanviar les claus de manera segura (normalment RSA o ECDH).
- Simètrica: un cop intercanviades les claus, es fa servir per xifrar la comunicació perquè és més eficient.
- Hashing: es fa servir per garantir la integritat de les dades mitjançant funcions com SHA-2 (en els HMAC, per exemple).

**WPA2 (protocol Wi-Fi)**

- Simètrica: es fa servir l'algoritme AES per xifrar les dades entre el dispositiu i el router.
- Hashing: s’utilitza en el procés d’autenticació per generar claus derivades a partir de la contrasenya (per exemple, amb PBKDF2) i també per verificar la integritat de les dades transmeses.

**Bitlocker/FileVault (encriptació de discs)**

- Simètrica: el disc s’encripta amb claus simètriques (normalment AES) perquè és més eficient per a grans volums de dades.

**Criptomonedes Blockchain (Bitcoin o ethereum)**

- Asimètrica: les claus públiques i privades (com ECDSA) s’utilitzen per signar transaccions i verificar-ne l’autenticitat.
- Hashing: es fa servir per enllaçar blocs (SHA-256 en Bitcoin), verificar la integritat de les dades i com a base del mecanisme de prova de treball (proof-of-work).

## 2. Sobre el protocol de comunicació HTTP

**Descriu com és la comunicació de peticions i respostes. Com estan compostos?**

Es basa en l’enviament de peticions amb un mètode (o verb) i, opcionalment, informació addicional. El servidor processa la petició i retorna una resposta amb un codi d’estat que indica el resultat de l’operació, i, també de forma opcional, informació en el cos de la resposta.

**Quins són els verbs més comuns a les sol·licituds i que volen dir?**

- Get - Demana informació sense editar-la o esborrar-la
- Delete - Esborra un recurs del servidor
- Patch - Modifica parcialment un recurs, canvia només una part
- Put - Modifica totalment un recurs (reemplaça)
- Post - Crea un nou recurs al servidor

**Determina el codi i quina informació en el body ha de retornar el servidor en els següents casos. Raona la resposta:**

- Una petició GET amb un Id i el recurs s’ha trobat.
  - Resposta 200 - Ok
  - Retorna un json amb l’informació del recurs:
  ```json
  {
    "id": 123,
    "nom": "Alex"
  }
  ```
**Una petició DELETE, on la BBDD ha fallat.**

    Resposta 500 - Internal server error

    Missatge d’error, ex:

    There was an internal error with the database

**Una petició PATCH on el recurs a modificar no existeix.**

    Resposta 404 - Not found

    Missatge d’error, ex:

    The resource was not found

**Una acció de login amb les dades incorrectes.**

    Resposta 401 - Unauthorized

    Missatge d’error, ex:

    Password or email were incorrect

**Una petició POST amb un rol no permés.**

    Resposta 403 - Forbidden

    Missatge d’error, ex:

    {Role} doesnt have permission

## 3. Realitza un quadre comparatiu entre websocket i un socket convencional. Quines tècniques i protocols de seguretat pots afegir a cada un?

|                            |                                                                   |                                                                      |
| -------------------------- | ----------------------------------------------------------------- | -------------------------------------------------------------------- |
|                            | **Web socket**                                                    | **Socket**                                                           |
| **Protocol**               | Inicia amb HTTP, després fa "upgrade" a WebSocket (sobre TCP)     | UDP o TCP                                                            |
| **Nivell**                 | Alt                                                               | Baix                                                                 |
| **Persistència**           | Connexió persistent i bidireccional                               | Persistent però gestionada manualment                                |
| **Usos**                   | Aplicacions en temps real( xats, jocs, etc)                       | Aplicacions de xarxa generals (FTP, SSH, etc)                        |
| **Encriptació**            | TLS                                                               | TLS (per TCP), DTLS (per UDP)                                        |
| **Autenticació**           | Headers HTTP, JWT, OAuth, Cookies                                 | Certificats, autenticació d’aplicació manual                         |
| **Tècniques de seguretat** | CORS, verificació d’origen, rate limiting, validació de missatges | Firewalls, IP whitelisting, xifrat personalitzat, autenticació mútua |

## 4. En un institut de formació professional es vol realitzar un portal per publicar treballs, apunts, notes i que funcioni com un canal de comunicació entre professors i alumnes. El canal de comunicació té forma de taulell de comentaris que admeten resposta. Aquest taulell és visible per alumnes i professors d’un mateix curs.

### Control d’accés: Fes una llista dels diferents rols. Per a cada rol especifica quins privilegis poden tenir sobre els diferents recursos i funcionalitats.

Professors - Crear, llegir i esborrar comentaris al taulell, afegir apunts i pràctiques, modificar notes dels alumnes dins del seu curs. Poden estar a múltiples cursos.

Alumnes - Només poden estar a un curs, poden crear comentaris al taulell  i veure activitats i activitats del taulell del seu curs, poden veure les seves notes i penjar treballs. No poden modificar el seu perfil.

Cap d’estudi - Poden crear nous cursos, assignar i canviar alumnes i professors als diferents cursos, poden crear posts als taulells dels diferents cursos, poden veure les dades dels alumnes pero no editar-les.

Secretaria - Poden crear i esborrar alumnes al sistema.

Desenvolupadors - Tenen tots els permisos que altres usuaris pero no poden veure les dades sensibles (Adreça, Compte corrent, telèfons, etc).

### Gestió de contrasenyes: Normes sobre la creació, ús i canvi periòdic de contrasenyes. Especifica normes segons el rol i raona les respostes.

Estudiants - Una majus mínim i nombres. 8 caràcters minim. Contrasenyes segures pero no massa complicades per tal de que no s'oblidin.

Professors - Una majus mínim, nombres i caràcters especials. 12 caràcters minim. Contrasenyes més segures però sense massa complicació.

Cap d’estudis, Secretaria i Desenvolupadors - Una majus mínim, nombres i caràcters especials. 18 caràcters minim. Contrasenyes segures i llargues per assegurar la seguretat del compte.

### Protecció de la informació: classifica les dades que s'emmagatzemen en 3 nivells segons la seva sensibilitat. Explica quin tractament i mesures de protecció ha de rebre cada nivell.

Baixa sensibilitat - Activitats, comentaris, apunts, etc 

Mitja sensibilitat - Notes, informació usuaris, entregas estudiants, etc

Alta sensibilitat - Contrasenyes i dades sensibles usuaris (informació bancaria, telefons)

### Còpies de seguretat (backups): Llista i explica diferents estratègies de còpies de seguretat es poden aplicar en aquest cas.

- Completa - Copia de tots els arxius

- Incremental - Còpia dels arxius canviats des de l'última copia

- Diferencial - Còpia dels arxius canviats des de l'última copia completa

## 5. L’empresa on treballes vol fer un event per presentar els seus nous productes a tots els clients. Per veure quants convidats vindran a l’event i quins clients responen t’han encarregat fer una API i un client web. El mateix client serà qui es registra a través del web. Els treballadors del departament de vendes (Relacions Públiques) podran gestionar els clients apuntats. Poden editar les dades dels clients. També hi ha administradors que poden editar i eliminar clients.

[Exercici 5](https://github.com/AlejandroMarEst/M09T1Serveis2aConvocatoria-MartinAlejandro/tree/feature/web-finished-web)

## 6. En la mateixa API i client anteriors crea un xat de text en temps real fent servir la llibreria SignalR.
  
[Exercici 6](https://github.com/AlejandroMarEst/M09T1Serveis2aConvocatoria-MartinAlejandro/tree/Exercici-6)

## 8. Enumera i explica els errors en el següent codi. Determina si compleix els principis de programació segura. En cas de no fer-ho raona el motiu i quin principi ha vulnerat.

   1. **Escriu el codi correcte seguint els principis de programació segura:**

```C#

           [HttpDelete("login")]
           public async Task<IActionResult> Login([FromBody] UserLoginDTO user)
           {
               var usuari = await _userManager.FindByEmailAsync(user.Email);
               if (usuari.Email != user.Email)
                   return Ok(“Error”);
               var claims = new List<Claim>()
               {
                    new Claim(ClaimTypes.Name, usuari.UserName),
                    new Claim(ClaimTypes.NameIdentifier, usuari.Id.ToString())
                };
                _logger.Information(“Usuari {usuari.UserName} amb id 
                {usuari.Id.ToString()} i password {usuari.password} ha fet logging 16             amb éxit!”);
    
                var token = CreateToken(claims.ToArray());
                return Ok(usuari);
            }
```

Errors: 
1.- No comprova la contrasenya en cap moment - Principi:

2.- Si comproves la contrasenya donaria igual ja que retorna ok igualment - Principi:

3.- Imprimeix la contrasenya al logger quan es fa el login correctament - Principi:

4.- Retorna la informacion sencera de l’usuari al acabar el login - Principi:

```C#
           [HttpDelete("login")]
           public async Task<IActionResult> Login([FromBody] UserLoginDTO user)
           {
               var usuari = await _userManager.FindByEmailAsync(user.Email);
               if (!await _userManager.CheckPasswordAsync(user, userDTO.Password))
                   return Unauthorized(ErrorMessages.InvalidEmailOrPassword);       
               var claims = new List<Claim>()
               {
                    new Claim(ClaimTypes.Name, usuari.UserName),
                    new Claim(ClaimTypes.NameIdentifier, usuari.Id.ToString())
                };
                _logger.Information(“Usuari {usuari.UserName} amb id 
                {usuari.Id.ToString()} ha fet logging amb éxit!”);
                var token = CreateToken(claims.ToArray());
                return Ok(token);
            }
```
