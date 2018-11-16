---
title: Workload 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Workload element
ms.assetid: 68ffd473-6546-4015-98d0-3763165de65c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 063a15a8278fa10e5c72326c7757ad4946b067f7
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51290729"
---
# <a name="workload-element-dta"></a>Workload 요소(DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  튜닝 세션에 사용할 작업을 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|각 **DTAInput** 요소에 한 번만 지정해야 합니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[데이터베이스 엔진 튜닝 관리자 시작 및 사용](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)|  
|**자식 요소**|[File 요소&#40;DTA&#41;](../../tools/dta/file-element-dta.md)<br /><br /> [Workload의 Database 요소&#40;DTA&#41;](../../tools/dta/database-element-for-workload-dta.md)<br /><br /> [EventString 요소&#40;DTA&#41;](../../tools/dta/eventstring-element-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 작업은 튜닝하려는 데이터베이스에 대해 실행되는 일련의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다. 데이터베이스 엔진 튜닝 관리자는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트, 추적 파일 및 추적 테이블을 작업으로 사용할 수 있습니다.  
  
 XML 입력 파일에 작업을 지정하고 **dta** 도구를 사용하여 명령줄에 작업을 지정할 경우 명령줄에 지정한 작업이 튜닝에 사용됩니다. 명령줄에 지정한 모든 튜닝 옵션은 XML 입력 파일에 지정된 옵션보다 우선 적용됩니다. 단, 사용자 지정 구성을 XML 입력 파일에 평가 모드로 입력할 경우는 예외입니다. 예를 들어 XML 입력 파일의 **Configuration** 요소에 구성이 입력되었고 또한 **EvaluateConfiguration** 요소가 튜닝 옵션 중 하나로 지정될 경우 XML 입력 파일에 지정된 튜닝 옵션은 명령줄에 입력한 튜닝 옵션보다 우선 적용됩니다.  
  
 각 튜닝 세션에 대해 하나의 작업을 지정해야 합니다.  
  
## <a name="example"></a>예제  
 다음 코드 예에서는 **Workload** 요소에 대한 **MyDatabase.MyDBOwner.TuningTable001** 추적 테이블을 지정합니다. **TuningTable001** 은 SQL Server 프로파일러로 튜닝 템플릿을 사용하여 추적 결과를 테이블로 저장하는 방식으로 작성되었습니다.  
  
```  
<DTAXML ...>  
  <DTAInput>  
    <Server>  
...code removed here...  
    </Server>  
    <Workload>  
      <Database>  
        <Name>MyDatabase</Name>  
        <Schema>  
          <Name>MyDBOwner</Name>  
            <Table>  
              <Name>TuningTable001</Name>  
            </Table>  
        </Schema>  
      </Database>  
    </Workload>  
...code removed here...  
  </DTAInput>  
</DTAXML>  
```  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
