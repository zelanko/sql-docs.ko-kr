---
title: "Synchronize 메서드 (RDS) | Microsoft Docs"
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Synchronize method [ADO]
ms.assetid: 7af42866-7db2-4174-8251-388a2cf741f2
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d223df00d0b32c3f608bcd61207de23da77e15cf
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="synchronize-method-rds"></a>Synchronize 메서드 (RDS)
2.5 이상 ADO에서 사용 하기 위해 연결 문자열에 지정 된 데이터베이스와 지정 된 레코드 집합을 동기화 합니다.  
  
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
object.Synchronize(ConnectionString As String, HandlerString As String, lSynchronizeOptions As Long, ppRecordset As Object, pStatusArray, [lcid As Long], [pInformation)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *ConnectionString*  
 요청 보낼 수 있는 OLE DB 공급자에 연결 하는 데 사용 하는 문자열입니다. 처리기를 사용 하는 경우 처리기 편집 하거나 연결 문자열을 바꿀 수 있습니다.  
  
 *HandlerString*  
 문자열이이 실행에서 사용 되는 처리기를 식별 합니다. 문자열에는 두 부분 포함 되어 있습니다. 첫 번째 부분은 사용할 처리기의 이름 (ProgID)을 포함 합니다. 두 번째 부분 문자열의 처리기에 전달 될 인수를 포함 합니다. 인수 문자열 해석 되는 방식을 특정 처리기입니다. 두 부분 (인수 문자열 추가 쉼표를 포함할 수 있습니다) 하지만 첫 번째 인스턴스의 문자열의 쉼표로 구분 됩니다. 인수는 선택적입니다.  
  
 *lSynchronizeOptions*  
 동기화 옵션의 비트 마스크입니다.  
  
 1 =*UpdateTransact* 트랜잭션에서 데이터베이스에 대 한 업데이트는 래핑됩니다. 업데이트 중 하나라도 실패 하면 트랜잭션은 중단 됩니다.  
  
 2 =*RefreshWithUpdate* 원인을 하지 않은 경우 반환 될 상태 행 *새로 고침* 나 *RefreshConflicts* 설정 됩니다.  
  
 4 =*새로 고침* 레코드 집합 데이터베이스에서 최신 데이터로 새로 고쳐집니다. 보류 중인 업데이트 된 데이터베이스에 푸시되 지 않습니다. 이 비트가 설정 되지 않으면 레코드 집합을 새로 고치지 않으면 및 보류 중인 모든 업데이트가 데이터베이스에 푸시됩니다.  
  
 8 =*RefreshConflicts* 보류 중인 변경 내용이 포함 된 모든 행이를 업데이트 하지 못했습니다. 업데이트 하지 못했습니다 행은 데이터베이스에서 최신 데이터로 새로 고쳐집니다.  
  
 *ppRecordset*  
 동기화 할 레코드 집합에 대 한 포인터입니다.  
  
 *pStatusArray*  
 행 상태에 대 한 영향을 받는 행의 안전 배열을 반환 하는 데 사용 되는 variant를 동기화 합니다. 다음 동기화 옵션을 모두 설정 된 경우를 설정 하지: *RefreshWithUpdate*, *새로 고침* 및 *RefreshConflicts*합니다.  
  
 *lcid*  
 LCID 작성 하는 데에 반환 되는 모든 오류 *pInformation*합니다.  
  
 *pInformation*  
 반환 된 정보 오류에 대 한 포인터 **Execute**합니다. NULL 인 경우에 오류 정보가 반환 됩니다.  
  
## <a name="remarks"></a>주의  
 *HandlerString* 매개 변수는 null 일 수 있습니다. 이 경우 어떻게 될까요 RDS 서버를 구성 하는 방법에 따라 달라 집니다. "MSDFMAP.handler" 처리기 문자열로 제공 하는 Microsoft 처리기 (Msdfmap.dll)을 사용 해야 함을 나타냅니다. "MASDFMAP.handler,sample.ini" 처리기 문자열로 Msdfmap.dll 처리기를 사용 해야 함을 "sample.ini" 인수를 처리기에 전달 해야 한다고 나타냅니다. 그런 다음 Msdfmap.dll를 사용 하 여 sample.ini 연결 및 쿼리 문자열을 검사 하는 방향으로 인수를 해석 합니다.  
  
## <a name="applies-to"></a>적용 대상  
 [DataFactory 개체(RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)


