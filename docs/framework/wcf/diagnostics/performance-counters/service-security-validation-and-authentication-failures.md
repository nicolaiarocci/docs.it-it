---
title: 'Servizio: Errori di convalida e di autenticazione della protezione'
ms.date: 03/30/2017
ms.assetid: 55c98268-b1ad-459d-851b-25ef52248187
ms.openlocfilehash: ba8da3ae6be6bd089690359f19e153da1e0b54fc
ms.sourcegitcommit: ccd8c36b0d74d99291d41aceb14cf98d74dc9d2b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/10/2018
ms.locfileid: "53150901"
---
# <a name="service-security-validation-and-authentication-failures"></a>Servizio: Errori di convalida e di autenticazione della protezione
Nome contatore: Errori di convalida e di autenticazione della protezione  
  
## <a name="description"></a>Descrizione  
 Questo contatore avanza ogni volta che un messaggio viene rifiutato a causa di un problema di sicurezza non coperto dal contatore "chiamate di sicurezza non autorizzate". Tra tali problemi si contano:  
  
-   Non è stato possibile leggere il token client dal messaggio.  
  
-   Il client token non è stato autenticato (ad esempio, la password era errata).  
  
-   La verifica della firma non è riuscita (ad esempio, il messaggio è stato manomesso).  
  
-   Il messaggio è un duplicato di un messaggio precedente. Ciò può verificarsi durante un attacco di tipo replay.  
  
-   Si è verificato un errore di decrittografia.  
  
-   Alcuni elementi obbligatori (ad esempio, timestamp mancante o blocco di dati crittografati) non sono presenti nel messaggio.  
  
-   Gli errori si sono verificati durante l'handshake TLSNEGO/SPNEGO.
