---
title: 오류 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
ms.assetid: bd0612f4-96ef-4919-b0f9-b5447210fe93
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4011730642355fb3161eed13428491e2692c9298
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48158983"
---
# <a name="errors"></a>오류
  OLE/COM 개체는 개체 멤버 함수의 HRESULT 반환 코드를 통해 오류를 보고합니다. OLE/COM HRESULT는 비트 압축 구조입니다. OLE는 구조 멤버를 역참조하는 매크로를 제공합니다.  
  
 OLE/COM은 **IErrorInfo** 인터페이스를 지정합니다. 이 인터페이스는 **GetDescription**과 같은 메서드를 제공합니다. 이 인터페이스를 사용하여 클라이언트는 OLE/COM 서버에서 오류 정보를 추출합니다. OLE DB는 단일 멤버 함수 실행에 대해 여러 개의 오류 정보 패킷 반환을 지원하기 위해 **IErrorInfo**를 확장합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 여러 오류를 반환합니다. 애플리케이션은 ISQLErrorInfo 및 IErrorRecords를 조합한 [IMultipleResults::GetResult](http://go.microsoft.com/fwlink/?LinkId=129630)를 호출하여 한 번에 하나씩 서버 오류를 검색할 수 있습니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 OLE DB 레코드로 향상 된 노출 **IErrorInfo**, 사용자 지정 `ISQLErrorInfo`, 및 공급자 관련 [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md) error 개체 인터페이스입니다.  
  
 오류 추적에 대한 자세한 내용은 [데이터 액세스 추적](http://go.microsoft.com/fwlink/?LinkId=125805)을 참조하십시오. 오류 추적에 추가 된 향상 된 기능에 대 한 내용은 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]를 참조 하십시오 [확장 이벤트 로그의 진단 정보 액세스](../native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [반환 코드](return-codes.md)  
  
-   [오류 인터페이스의 정보](information-in-error-interfaces.md)  
  
-   [SQL Server 오류 세부 정보](sql-server-error-detail.md)  
  
-   [오류 정보 검색](retrieving-error-information.md)  
  
-   [SQL Server 메시지 결과](sql-server-message-results.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client&#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
