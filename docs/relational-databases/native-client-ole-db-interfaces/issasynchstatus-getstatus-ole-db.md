---
description: 'ISSAsynchStatus:: GetStatus (Native Client OLE DB 공급자)'
title: 'ISSAsynchStatus:: GetStatus (Native Client OLE DB 공급자) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAsynchStatus::GetStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- GetStatus method
ms.assetid: 354b6ee4-b5a1-48f6-9403-da3bdc911067
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4dec7256e445ff41f5e8549e4dff4e6c5c341fe1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469384"
---
# <a name="issasynchstatusgetstatus-native-client-ole-db-provider"></a>ISSAsynchStatus:: GetStatus (Native Client OLE DB 공급자)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  비동기적으로 실행 중인 작업의 상태를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
HRESULT GetStatus(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation,  
        DBCOUNTITEM *pulProgress,  
        DBCOUNTITEM *pulProgressMax,  
        DBASYNCHPHASE *peAsynchPhase,  
        LPOLESTR *ppwszStatusText);  
```  
  
## <a name="arguments"></a>인수  
 *hChapter*[in]  
 장 핸들입니다. 폴링되는 개체가 행 집합 개체가 아니거나 작업이 장에 적용되지 않는 경우 이 값을 공급자가 무시하는 DB_NULL_HCHAPTER로 설정해야 합니다.  
  
 *eOperation*[in]  
 비동기 상태가 요청되는 작업입니다. 값은 다음과 같아야 합니다.  
  
 DBASYNCHOP_OPEN - 소비자가 행 세트의 비동기 열기 또는 채우기나 데이터 원본 개체의 비동기 초기화에 대한 정보를 요청합니다. 공급자가 직접 URL 바인딩을 지원하는 OLE DB 2.5 규격 공급자이면 소비자는 데이터 원본, 행 집합, 행 또는 스트림 개체의 비동기 초기화나 채우기에 대한 정보를 요청합니다.  
  
 *pulProgress*[out]  
 *pulProgressMax* 매개 변수에 표시된 예상 최대값을 기준으로 비동기 작업의 현재 진행률을 반환할 메모리에 대한 포인터입니다. *pulProgress* 의 의미에 대한 자세한 내용은 *peAsynchPhase* 설명을 참조하십시오.  
  
 *pulProgress* 가 Null 포인터이면 진행률이 반환되지 않습니다.  
  
 *pulProgressMax*[out]  
 *pulProgress* 매개 변수의 예상 최대값을 반환할 메모리에 대한 포인터입니다. 이 메서드에 대한 호출에서 이 값이 변경될 수도 있습니다. *pulProgressMax* 의 의미에 대한 자세한 내용은 *peAsynchPhase* 설명을 참조하십시오.  
  
 *pulProgressMax* 가 Null 포인터이면 예상 최대값이 반환되지 않습니다.  
  
 *peAsynchPhase*[out]  
 비동기 작업의 진행률과 관련해서 추가 정보를 반환할 메모리에 대한 포인터입니다. 유효한 값은 다음과 같습니다.  
  
 DBASYNCHPHASE_INITIALIZATION - 개체가 초기화 단계에 있습니다. *pulProgress* 및 *pulProgressMax* 인수는 예상 완료율을 나타냅니다. 개체가 완전히 구체화되지 않았습니다. 다른 인터페이스를 호출하려는 시도가 실패할 수 있으며, 개체에서 전체 인터페이스 집합을 사용하지 못할 수도 있습니다. 행을 업데이트, 삭제 또는 삽입하는 명령에 대한 **ICommand::Execute** 호출 결과로 비동기 작업이 수행되었으며 *cParamSets* 가 1보다 큰 경우 *pulProgress* 및 *pulProgressMax* 는 단일 매개 변수 집합이나 전체 매개 변수 집합 배열의 진행률을 나타낼 수 있습니다.  
  
 DBASYNCHPHASE_POPULATION - 개체가 채우기 단계에 있습니다. 행 집합이 완전히 초기화되었으며 개체에서 모든 인터페이스를 사용할 수 있지만 행 집합에 채워지지 않은 추가 행이 있을 수 있습니다. *pulProgress* 및 *pulProgressMax* 는 채워지는 행 수에 따라 지정될 수도 있지만 일반적으로 행 집합을 채우는 데 필요한 시간이나 노력을 기반으로 지정됩니다. 따라서 호출자는 이 정보를 최종 행 수가 아니라 프로세스에 걸리는 시간의 대략적인 예상 값으로 사용합니다. 이 단계는 행 집합을 채우는 동안에만 반환되며, 데이터 원본 개체의 초기화나 행을 업데이트, 삭제 또는 삽입하는 명령 실행에서는 반환되지 않습니다.  
  
 DBASYNCHPHASE_COMPLETE - 개체의 모든 비동기 처리가 완료되었습니다. **ISSAsynchStatus::GetStatus** 는 작업 결과를 나타내는 HRESULT를 반환합니다. 일반적으로 이것은 작업을 동기적으로 호출한 경우에 반환되는 HRESULT입니다. 행을 업데이트, 삭제 또는 삽입하는 명령에 대한 **ICommand::Execute** 호출 결과로 비동기 작업이 수행된 경우 *pulProgress* 및 *pulProgressMax* 는 해당 명령이 적용된 총 행 수와 같습니다. *cParamSets* 가 1보다 크면 이 값은 실행 시 지정한 모든 매개 변수 집합이 적용된 총 행 수입니다. *peAsynchPhase* 가 Null 포인터이면 상태 코드가 반환되지 않습니다.  
  
 DBASYNCHPHASE_CANCELED - 개체의 비동기 처리가 중단되었습니다. **ISSAsynchStatus::GetStatus** 에서 DB_E_CANCELED를 반환합니다. 행을 업데이트, 삭제 또는 삽입하는 명령에 대한 **ICommand::Execute** 호출 결과로 비동기 작업이 수행된 경우 *pulProgress* 는 취소 전에 해당 명령의 영향을 받는 모든 매개 변수 집합에 대한 총 행 수와 같습니다.  
  
 *ppwszStatusText*[in/out]  
 작업에 대한 추가 정보가 포함된 메모리에 대한 포인터입니다. 공급자는 이 값을 사용하여 작업의 서로 다른 요소(예: 액세스되는 다른 리소스)를 구분할 수 있습니다. 이 문자열은 데이터 원본 개체의 DBPROP_INIT_LCID 속성에 따라 지역화됩니다.  
  
 *ppwszStatusText* 가 입력 시 Null이 아니면 공급자는 *ppwszStatusText* 로 식별된 특정 요소와 연결된 상태를 반환합니다. *ppwszStatusText* 가 *eOperation* 의 요소를 나타내지 않으면 공급자는 *pulProgress* 및 *pulProgressMax* 를 같은 값으로 설정하여 S_OK를 반환합니다. 공급자는 텍스트 식별자를 기반으로 요소를 구분하지 않는 경우 *ppwszStatusText* 를 NULL로 설정하고 작업 전체에 대한 정보를 반환합니다. 그렇지 않고 *ppwszStatusText* 가 입력 시 Null이 아니면 공급자는 *ppwszStatusText* 를 그대로 둡니다.  
  
 *ppwszStatusText* 가 입력 시 Null이면 공급자는 *ppwszStatusText* 를 특정 값으로 설정하여 작업에 대한 추가 정보를 나타내거나, 해당 정보를 사용할 수 없는 경우 또는 **ISSAsynchStatus::GetStatus** 에서 오류를 반환하는 경우 NULL로 설정합니다. *ppwszStatusText* 가 입력 시 Null이면 공급자는 상태 문자열에 대해 메모리를 할당하고 이 메모리에 대한 주소를 반환합니다. 해당 문자열이 더 이상 필요하지 않은 경우 소비자는 **IMalloc::Free** 를 사용하여 이 메모리를 해제합니다.  
  
 *ppwszStatusText* 가 입력 시 NULL이면 상태 문자열이 반환되지 않으며 공급자가 작업 요소나 일반적인 작업에 대한 정보를 반환합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공적으로 반환했습니다.  
  
-   *peAsynchPhase* 가 DBASYNCHPHASE_INITIALIZATION과 같으면 개체가 완전히 초기화되지 않았으며 다른 인터페이스를 호출하려는 시도가 실패할 수 있고 개체에서 전체 인터페이스 집합을 사용하지 못할 수도 있습니다.  
  
-   *peAsynchPhase* 가 DBASYNCHPHASE_POPULATION과 같으면 행 집합이 완전히 초기화된 것이며 개체에서 모든 인터페이스를 사용할 수 있습니다. 하지만 아직 행 집합에 채워지지 않은 추가 행이 있을 수 있습니다.  
  
-   *peAsynchPhase* 가 DBASYNCHPHASE_COMPLETE와 같으면 개체의 모든 비동기 처리가 완료되었습니다. 개체가 완전히 초기화되었으며 채워졌습니다.  
  
 DB_E_CANCELED  
 행 집합을 채우는 동안 비동기 처리가 취소되었습니다. 채우기가 중지되지만 행 집합은 이미 채워진 행에 대해 유효합니다.  
  
 데이터 원본 개체가 초기화되는 동안 비동기 처리가 취소되었습니다. 데이터 원본 개체의 초기화가 취소되지 않은 상태입니다.  
  
 E_INVALIDARG  
 *hChapter* 매개 변수가 잘못되었습니다.  
  
 E_UNEXPECTED  
 **ISSAsynchStatus::GetStatus** 가 데이터 원본 개체에서 호출되었으며, **IDBInitialize::Initialize** 는 데이터 원본 개체에서 호출되지 않았습니다.  
  
 **ISSAsynchStatus::GetStatus** 가 행 집합에서 호출되고 **ITransaction::Commit** 또는 **ITransaction::Abort** 가 호출되었으며 개체가 좀비 상태에 있습니다.  
  
 초기화 단계에서 비동기적으로 취소된 행 집합에서 **ISSAsynchStatus::GetStatus** 가 취소되었습니다. 행 집합이 좀비 상태에 있습니다.  
  
 E_FAIL  
 공급자 관련 오류가 발생했습니다.  
  
## <a name="remarks"></a>설명  
 **ISSAsynchStatus::GetStatus** 메서드는 데이터 원본 개체의 초기화가 중단될 경우 DB_E_CANCELED 대신 E_UNEXPECTED가 반환된다는 점만 제외하고 **IDBAsynchStatus::GetStatus** 메서드와 동일하게 동작합니다. 단, [ISSAsynchStatus::WaitForAsynchCompletion](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)은 DB_E_CANCELED를 반환합니다. 이는 추가적인 초기화 작업이 시도될 수 있도록 중단 이후 데이터 원본 개체가 평소의 좀비 상태로 유지되지 않기 때문입니다.  
  
 행 집합이 비동기적으로 초기화되거나 채워진 경우 이 메서드를 지원해야 합니다.  
  
 표시된 반환 값 외에도 **ISSAsynchStatus::GetStatus** 는 비동기 작업을 시작한 메서드에 의해 반환되어 작업의 성공 또는 실패를 나타내는 모든 HRESULT를 반환할 수 있습니다.  
  
 일부 비동기 작업은 "완료됨" 및 "완료되지 않음"을 제외한 다른 상태를 반환할 수 없습니다. 예측의 가부만 나타내도록 *pulProgressMax* 를 값 1로 설정해야 하므로 해당 응답은 0/1 또는 1/1이 됩니다.  
  
 태스크 완료도 예측의 개선을 반영하는 경우 공급자가 연속 호출에서 *pulProgressMax* 를 변경하고 이전보다 더 작은 비율을 반환할 수도 있습니다.  
  
 공급자가 추가 정확성을 보장할 의무는 없지만 합리적인 완료 예측이 가능한 경우 이렇게 하는 것이 좋습니다. 이 함수는 주로 진행 상황에 대한 피드백을 사용자에게 제공하기 위한 것이므로 이러한 노력을 통해 사용자 인터페이스 품질이 향상됩니다. 보이지 않는 장기 실행 태스크에 대한 피드백의 품질이 향상되면 사용자 만족도가 증가합니다.  
  
 초기화된 데이터 원본 개체나 채워진 행 집합에서 **ISSAsynchStatus::GetStatus** 를 호출하거나 *eOperation* 에 대해 DBASYNCHOP_OPEN 이외의 값을 전달하면 *pulProgress* 및 *pulProgressMax* 를 동일한 값으로 설정하여 S_OK가 반환됩니다. 행을 업데이트, 삭제 또는 삽입하는 명령을 실행하여 만든 개체에서 **ISSAsynchStatus::GetStatus** 를 호출하는 경우 *pulProgress* 및 *pulProgressMax* 는 모두 해당 명령이 적용된 총 행 수를 나타냅니다.  
  
## <a name="see-also"></a>참고 항목  
 [비동기 작업 수행](../../relational-databases/native-client/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
