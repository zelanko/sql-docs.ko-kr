---
title: Synchronize 메서드 (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Synchronize method [ADO]
ms.assetid: 7af42866-7db2-4174-8251-388a2cf741f2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e280e5f8c9eda472c6448b199ffa94ac18c13751
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67963261"
---
# <a name="synchronize-method-rds"></a>Synchronize 메서드(RDS)
지정 된 레코드 집합을 ADO 2.5 이상에서 사용 하기 위해 연결 문자열에 지정 된 데이터베이스와 동기화 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.Synchronize(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray, [lcid As Long], [pInformation)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ConnectionString*  
 요청이 전송 되는 OLE DB 공급자에 연결 하는 데 사용 되는 문자열입니다. 처리기를 사용 하는 경우 처리기는 연결 문자열을 편집 하거나 바꿀 수 있습니다.  
  
 *HandlerString*  
 문자열은이 실행에 사용할 처리기를 식별 합니다. 문자열에는 두 부분이 포함 됩니다. 첫 번째 부분에는 사용할 처리기의 이름 (ProgID)이 포함 되어 있습니다. 문자열의 두 번째 부분에는 처리기에 전달 될 인수가 들어 있습니다. 인수 문자열을 해석 하는 방법은 handler와 관련이 있습니다. 두 부분은 문자열에서 쉼표의 첫 번째 인스턴스로 구분 됩니다 (인수 문자열에 추가 쉼표를 포함할 수 있지만). 인수는 선택 사항입니다.  
  
 *lSynchronizeOptions*  
 동기화 옵션의 비트 마스크입니다.  
  
 1 = 데이터베이스에 대 한*UpdateTransact* 업데이트가 트랜잭션에 래핑됩니다. 업데이트가 실패 하는 경우 트랜잭션이 중단 됩니다.  
  
 2 =*Refreshwithupdate* 를 수행 하면 *새로 고침* 및 *refresh충돌과* 모두 설정 되지 않은 경우 행 상태가 반환 됩니다.  
  
 4 =*새로 고침* 레코드 집합은 데이터베이스의 현재 데이터로 새로 고쳐집니다. 보류 중인 업데이트는 데이터베이스로 푸시되 지 않습니다. 이 비트가 설정 되지 않은 경우에는 레코드 집합을 새로 고치지 않으며 보류 중인 업데이트가 데이터베이스에 푸시됩니다.  
  
 8 =*refreshconflicts 충돌* 하는 변경 내용이 있는 모든 행이 업데이트 되지 않습니다. 업데이트 하지 못한 행은 데이터베이스의 현재 데이터로 새로 고쳐집니다.  
  
 *ppRecordset*  
 동기화 할 레코드 집합에 대 한 포인터입니다.  
  
 *pStatusArray*  
 동기화의 영향을 받는 행의 안전 행 상태 배열을 반환 하는 데 사용 되는 variant입니다. 다음 동기화 옵션이 설정 되지 않은 경우에는 *Refreshwithupdate*, *Refresh* 및 *refresh충돌과*같이 설정 되지 않습니다.  
  
 *lcid*  
 *Pinformation*에서 반환 되는 오류를 작성 하는 데 사용 되는 LCID입니다.  
  
 *pInformation*  
 **Execute**에서 반환 된 정보 오류에 대 한 포인터입니다. NULL 인 경우에는 오류 정보가 반환 되지 않습니다.  
  
## <a name="remarks"></a>설명  
 *Handlerstring* 매개 변수는 null 일 수 있습니다. 이 경우에 발생 하는 상황은 RDS 서버를 구성 하는 방법에 따라 달라 집니다. "MSDFMAP. handler"의 처리기 문자열은 Microsoft에서 제공 하는 처리기 (Msdfmap .dll)를 사용 해야 함을 나타냅니다. "MASDFMAP, .sample"의 처리기 문자열은 Msdfmap .dll 처리기를 사용 해야 하며 "sample. .ini" 인수를 처리기에 전달 해야 함을 나타냅니다. 그러면 msdfmap .dll에서 .sample을 사용 하 여 연결 및 쿼리 문자열을 확인 하는 방향으로 인수를 해석 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataFactory 개체(RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


