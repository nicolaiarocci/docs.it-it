---
title: 'Procedura: Eliminare una chiave del Registro di sistema in Visual Basic'
ms.date: 07/20/2015
f1_keywords:
- vb.DeleteSetting
helpviewer_keywords:
- GetSetting function [Visual Basic]
- registry [Visual Basic], deleting values
- GetAllSettings function
- registry keys [Visual Basic], deleting
- registry [Visual Basic], deleting keys
- examples [Visual Basic], registry
ms.assetid: ab9aca0e-42b0-4ff7-8ff9-845a4bfdf9f2
ms.openlocfilehash: fdb61fee8a790000c53b6c9a0188999bc0cb09ae
ms.sourcegitcommit: 0be8a279af6d8a43e03141e349d3efd5d35f8767
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/18/2019
ms.locfileid: "58840333"
---
# <a name="how-to-delete-a-registry-key-in-visual-basic"></a>Procedura: Eliminare una chiave del Registro di sistema in Visual Basic
È possibile usare i metodi <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%28System.String%29> e <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%28System.String%2CSystem.Boolean%29> per eliminare le chiavi del Registro di sistema.  
  
## <a name="procedure"></a>Routine  
  
#### <a name="to-delete-a-registry-key"></a>Per eliminare una chiave del Registro di sistema  
  
-   Usare il metodo `DeleteSubKey` per eliminare una chiave del Registro di sistema. Questo esempio elimina la chiave Software/TestApp nell'hive CurrentUser. È possibile impostarlo nel codice sulla stringa appropriata oppure basarsi sulle informazioni specificate dall'utente.  
  
     [!code-vb[VbResourceTasks#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbResourceTasks/VB/Class1.vb#19)]  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Il metodo `DeleteSubKey` restituisce una stringa vuota se la coppia chiave/valore non esiste.  
  
 Le seguenti condizioni possono generare un'eccezione:  
  
-   Il nome della chiave è `Nothing` (<xref:System.ArgumentNullException>).  
  
-   L'utente non è autorizzato a eliminare le chiavi del Registro di sistema (<xref:System.Security.SecurityException>).  
  
-   Il nome della chiave supera il limite di 255 caratteri (<xref:System.ArgumentException>).  
  
-   La chiave del Registro di sistema è di sola lettura (<xref:System.UnauthorizedAccessException>).  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 Le chiamate al Registro di sistema hanno esito negativo se non sono concesse autorizzazioni sufficienti in fase di esecuzione (<xref:System.Security.Permissions.RegistryPermission>) o se, in base a quanto determinato dagli ACL, l'utente non usa l'accesso corretto per la creazione o la scrittura nelle impostazioni. Ad esempio, un'applicazione locale che ha l'autorizzazione di sicurezza dall'accesso di codice potrebbe non avere l'autorizzazione del sistema operativo.  
  
## <a name="see-also"></a>Vedere anche

- <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%2A>
- <xref:Microsoft.Win32.RegistryKey.DeleteSubKey%2A>
- <xref:Microsoft.Win32.RegistryKey>
- [Sicurezza e Registro di sistema](../../../../visual-basic/developing-apps/programming/computer-resources/security-and-the-registry.md)
- [Lettura e scrittura nel Registro di sistema](../../../../visual-basic/developing-apps/programming/computer-resources/reading-from-and-writing-to-the-registry.md)
