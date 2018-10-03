---
title: SQL Server Native Client OLE DB 공급자 응용 프로그램 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ab956213d87a39eaa8676324fdf99f860b167f1d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47712495"
---
# <a name="creating-a-sql-server-native-client-ole-db-provider-application"></a>SQL Server Native Client OLE DB 공급자 응용 프로그램 만들기
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  만들기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 응용 프로그램에 이러한 단계가 포함 됩니다.  
  
1.  데이터 원본에 대한 연결 설정  
  
2.  명령 실행  
  
3.  결과 처리  
  
> [!NOTE]  
>  가능하면 Windows 인증을 사용하세요. Windows 인증을 사용할 수 없으면 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 자격 증명은 파일에 저장하지 않는 것이 좋습니다. 자격 증명을 유지하려면 [the Win32 cryptoAPI](http://go.microsoft.com/fwlink/?LinkId=9504)를 사용하여 자격 증명을 암호화해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [데이터 원본에 대한 연결 설정](../../relational-databases/native-client-ole-db-provider/establishing-a-connection-to-a-data-source.md)  
  
-   [명령 실행](../../relational-databases/native-client-ole-db-provider/executing-a-command.md)  
  
-   [결과 처리](../../relational-databases/native-client-ole-db-provider/processing-results.md)  
  
-   [OLE DB 속성 정보](../../relational-databases/native-client-ole-db-provider/about-ole-db-properties.md)  
  
-   [SQL Server Native Client의 OLE DB에서 OUTPUT 절 사용](../../relational-databases/native-client-ole-db-provider/using-the-output-clause-with-ole-db-in-sql-server-native-client.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
