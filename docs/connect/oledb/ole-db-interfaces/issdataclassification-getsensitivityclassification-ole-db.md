---
title: ISSDataClassification::GetSensitivityClassification | Microsoft Docs
description: ISSDataClassification::GetSensitivityClassification
ms.custom: ''
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSDataClassification::GetSensitivityClassification
apitype: COM
helpviewer_keywords:
- GetSensitivityClassification method
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: 04877e626b57022d0110501b7da6145b2c4997d2
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506672"
---
# <a name="issdataclassificationgetsensitivityclassification"></a>ISSDataClassification::GetSensitivityClassification
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../../includes/applies-to-version/sql-asdb-asa.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  활성 행 집합의 민감도 분류 데이터를 검색합니다. 자세한 내용 및 코드 샘플은 [데이터 분류 사용](../features/using-data-classification.md)을 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```  
HRESULT GetSensitivityClassification(
    SENSITIVITYCLASSIFICATION** ppSensitivityClassification);
```  
  
## <a name="arguments"></a>인수  
  *ppSensitivityClassification*[out]  
 SENSITIVITYCLASSIFICATION 구조체 포인터에 대한 포인터입니다. 메서드가 실패하거나 사용할 수 있는 데이터 분류 정보가 없는 경우 공급자는 메모리를 할당하지 않고 출력에서 ppSensitivityClassification 인수가 null 포인터인지 확인합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 S_OK  
 메서드가 성공했습니다.    
  
 E_INVALIDARG  
 *ppSensitivityClassification* 인수가 NULL입니다.  
  
 E_OUTOFMEMORY  
 OLE DB Driver for SQL Server에서 요청을 완료하기에 충분한 메모리를 할당할 수 없습니다.  

  
## <a name="remarks"></a>설명  
OLE DB Driver for SQL Server는 SENSITIVITYCLASSIFICATION 구조체와 이 구조체가 참조하는 데이터를 보유할 메모리 블록을 할당합니다. 소비자가 더 이상 분류 데이터에 액세스할 필요가 없게 되면 [IMalloc::Free](https://docs.microsoft.com/windows/win32/api/objidl/nf-objidl-imalloc-free) 메서드를 호출하여 이 메모리의 할당을 취소해야 합니다.  
  
 SENSITIVITYCLASSIFICATION 구조체는 다음과 같이 정의됩니다.
  
```cpp
typedef struct tagSensitivityClassification
{
    USHORT                     cSensitivityLabels;
    SENSITIVITYLABEL          *rgSensitivityLabels;
    USHORT                     cInformationTypes;
    INFORMATIONTYPE           *rgInformationTypes;
    USHORT                     cColumnSensitivityMetadata;
    COLUMNSENSITIVITYMETADATA *rgColumnSensitivityMetadata;
    SENSITIVITYRANKENUM        eQuerySensitivityRank;
} SENSITIVITYCLASSIFICATION;
```  

|멤버|설명|  
|------------|-----------------|  
|*cSensitivityLabels*|*rgSensitivityLabels* 의 SENSITIVITYLABEL 구조체 수입니다.|  
|*rgSensitivityLabels*|SENSITIVITYLABEL 구조체의 배열입니다.|  
|*cInformationTypes*|*rgInformationTypes* 의 INFORMATIONTYPE 구조체 수입니다.|  
|*rgInformationTypes*|INFORMATIONTYPE 구조체의 배열입니다.|  
|*cColumnSensitivityMetadata*|*rgColumnSensitivityMetadata* 의 COLUMNSENSITIVITYMETADATA 구조체 수입니다.|  
|*rgColumnSensitivityMetadata*|COLUMNSENSITIVITYMETADATA 구조체의 배열입니다.|  
|*eQuerySensitivityRank*|행 집합을 가져오기 위해 실행된 쿼리의 상대적인 민감도 순위입니다.|  

SENSITIVITYLABEL 구조체는 다음과 같이 정의됩니다.
```cpp
typedef struct tagSENSITIVITYLABEL
{
    LPOLESTR pwszName;
    LPOLESTR pwszId;
} SENSITIVITYLABEL;
```

|멤버|설명|  
|------------|-----------------|  
|*pwszName*|민감도 레이블의 이름입니다.|  
|*pwszId*|민감도 레이블의 식별자입니다.|  

INFORMATIONTYPE 구조체는 다음과 같이 정의됩니다.
```cpp
typedef struct tagINFORMATIONTYPE
{
    LPOLESTR pwszName;
    LPOLESTR pwszId;
} INFORMATIONTYPE;
```

|멤버|설명|  
|------------|-----------------|  
|*pwszName*|정보 유형의 이름입니다.|  
|*pwszId*|정보 유형의 식별자입니다.|  

COLUMNSENSITIVITYMETADATA 구조체는 다음과 같이 정의됩니다.
```cpp
typedef struct tagCOLUMNSENSITIVITYMETADATA
{
    SENSITIVITYPROPERTY* rgSensitivityProperties;
    USHORT cSensitivityProperties;
} COLUMNSENSITIVITYMETADATA;
```

|멤버|설명|  
|------------|-----------------|  
|*cSensitivityProperties*|*rgSensitivityProperties* 의 SENSITIVITYPROPERTY 구조체 수입니다.|  
|*rgSensitivityProperties*|SENSITIVITYPROPERTY 구조체의 배열입니다.|  

SENSITIVITYRANKENUM 열거형은 다음과 같이 정의됩니다.
```cpp
typedef enum tagSENSITIVITYRANKENUM
{
    SENSITIVITYRANK_NOT_DEFINED = -1,
    SENSITIVITYRANK_NONE = 0,
    SENSITIVITYRANK_LOW = 10,
    SENSITIVITYRANK_MEDIUM = 20,
    SENSITIVITYRANK_HIGH = 30,
    SENSITIVITYRANK_CRITICAL = 40
} SENSITIVITYRANKENUM;
```

SENSITIVITYPROPERTY 구조체는 다음과 같이 정의됩니다.
```cpp
typedef struct tagSENSITIVITYPROPERTY
{
    SENSITIVITYLABEL* pSensitivityLabel;
    INFORMATIONTYPE* pInformationType;
    SENSITIVITYRANKENUM eSensitivityRank;
} SENSITIVITYPROPERTY;
```

|멤버|설명|  
|------------|-----------------|  
|*pSensitivityLabel*|SENSITIVITYLABEL 구조체에 대한 포인터입니다.|  
|*pInformationType*|INFORMATIONTYPE 구조체에 대한 포인터입니다.|  
|*eSensitivityRank*|열별 데이터의 일부인 열의 상대적인 민감도 순위입니다.|  

## <a name="see-also"></a>참고 항목  
 [ISSDataClassification](../../oledb/ole-db-interfaces/issdataclassification-ole-db.md)  
 [행 집합](../ole-db-rowsets/rowsets.md)  
  
