---
title: SQL Server Native Client OLE DB 공급자 응용 프로그램 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, application creation
- applications [SQL Server Native Client]
- OLE DB, creating applications
ms.assetid: f3ae6815-f32d-4913-a1a2-2ba2f20cfd88
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e422ac6535900a287ae610a85241dc67172c4f7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63209756"
---
# <a name="creating-a-sql-server-native-client-ole-db-provider-application"></a>SQL Server Native Client OLE DB 공급자 애플리케이션 만들기
  Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB 공급자 응용 프로그램을 만들려면 다음 단계를 수행 해야 합니다.  
  
1.  데이터 원본에 대한 연결 설정  
  
2.  명령 실행  
  
3.  결과 처리  
  
> [!NOTE]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지하려면 [the Win32 cryptoAPI](https://go.microsoft.com/fwlink/?LinkId=9504)를 사용하여 자격 증명을 암호화해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [데이터 원본에 대한 연결 설정](establishing-a-connection-to-a-data-source.md)  
  
-   [명령 실행](executing-a-command.md)  
  
-   [결과 처리](processing-results.md)  
  
-   [OLE DB 속성 정보](about-ole-db-properties.md)  
  
-   [SQL Server Native Client의 OLE DB에서 OUTPUT 절 사용](using-the-output-clause-with-ole-db-in-sql-server-native-client.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
