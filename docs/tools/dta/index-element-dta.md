---
title: Index 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Index element (DTA)
ms.assetid: 447d3964-b387-40f6-9189-71386774c29e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fdbe54ce16b8ee0ed441bfcf7098d28004d482d2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620251"
---
# <a name="index-element-dta"></a>Index 요소(DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  사용자 지정 구성에 대해 만들거나 삭제하려는 인덱스에 대한 정보를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Recommendation>  
  <Create>  
    <Index [Clustered | Unique | Online | IndexSizeInMB | NumberOfRows             | QUOTED_IDENTIFIER | ARITHABORT | CONCAT_NULL_YIELDS_NULL             | ANSI_NULLS | ANSI_PADDING | ANSI_WARNINGS  
            | NUMERIC_ROUNDABORT]  
     ...code removed here...  
    </Index>  
```  
  
## <a name="element-attributes"></a>요소 특성  
  
|인덱스 특성|데이터 형식|설명|  
|---------------------|---------------|-----------------|  
|**클러스터형**|**boolean**|(선택 사항) 클러스터형 인덱스를 지정합니다. "true" 또는 "false"로 설정합니다. 예를 들면 다음과 같습니다.<br /><br /> `<Index Clustered="true">`<br /><br /> 기본적으로 이 특성은 "false"로 설정됩니다.|  
|**고유**|**boolean**|(선택 사항) 고유 인덱스를 지정합니다. "true" 또는 "false"로 설정합니다. 예를 들면 다음과 같습니다.<br /><br /> `<Index Unique="true">`<br /><br /> 기본적으로 이 특성은 "false"로 설정됩니다.|  
|**온라인**|**boolean**|(선택 사항) 서버가 온라인 상태인 동안에 작업을 수행할 수 있는 인덱스를 지정하며 임시 디스크 공간이 필요합니다. "true" 또는 "false"로 설정합니다. 예를 들면 다음과 같습니다.<br /><br /> `<Index Online="true">`<br /><br /> 기본적으로 이 특성은 "false"로 설정됩니다.<br /><br /> 자세한 내용은 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)을 참조하세요.|  
|**IndexSizeInMB**|**double**|(선택 사항) 인덱스의 최대 크기(MB)를 지정합니다. 예를 들면 다음과 같습니다.<br /><br /> `<Index IndexSizeInMB="873.75">`<br /><br /> 기본 설정은 없습니다.|  
|**NumberOfRows**|**integer**|(선택 사항) 다른 테이블 크기를 효과적으로 시뮬레이트하는 다른 인덱스 크기를 시뮬레이트합니다. 예를 들면 다음과 같습니다.<br /><br /> `<Index NumberOfRows="3000">`<br /><br /> 기본 설정은 없습니다.|  
|**QUOTED_IDENTIFIER**|**boolean**|(선택 사항) [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 인용 부호 구분 식별자 및 리터럴 문자열에 관해 ISO 규칙을 따르도록 합니다. 인덱스가 계산 열 또는 뷰에 있는 경우 이 특성을 설정해야 합니다. 예를 들어 다음 구문은 이 특성을 설정합니다.<br /><br /> `<Index QUOTED_IDENTIFIER [...]>`<br /><br /> 기본적으로 이 특성은 해제되어 있습니다.<br /><br /> 자세한 내용은 [SET QUOTED_IDENTIFIER&#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)를 참조하세요.|  
|**ARITHABORT**|**boolean**|(선택 사항) 쿼리 실행 중 오버플로 또는 0으로 나누기 오류가 발생하면 쿼리를 종료합니다. 인덱스가 계산 열 또는 뷰에 있는 경우 이 특성을 설정해야 합니다. 예를 들어 다음 구문은 이 특성을 설정합니다.<br /><br /> `<Index ARITHABORT [...]>`<br /><br /> 기본적으로 이 특성은 해제되어 있습니다.<br /><br /> 자세한 내용은 [SET ARITHABORT&#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)를 참조하세요.|  
|**CONCAT_NULL_YIELDS_**<br /><br /> **NULL**|**boolean**|(선택 사항) 연결 결과를 Null 값으로 처리할지 빈 문자열 값으로 처리할지 여부를 제어합니다. 인덱스가 계산 열 또는 뷰에 있는 경우 이 특성을 설정해야 합니다. 예를 들어 다음 구문은 이 특성을 설정합니다.<br /><br /> `<Index CONCAT_NULL_YIELDS_NULL [...]>`<br /><br /> 기본적으로 이 특성은 해제되어 있습니다.<br /><br /> 자세한 내용은 [SET CONCAT_NULL_YIELDS_NULL&#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)을 참조하세요.|  
|**ANSI_NULLS**|**boolean**|(선택 사항) 같음(=)과 같지 않음(<>) 비교 연산자를 Null 값과 함께 사용할 경우의 ISO 호환 동작을 지정합니다. 인덱스가 계산 열 또는 뷰에 있는 경우 이 특성을 설정해야 합니다. 예를 들어 다음 구문은 이 특성을 설정합니다.<br /><br /> `<Index ANSI_NULLS [...]>`<br /><br /> 기본적으로 이 특성은 해제되어 있습니다.<br /><br /> 자세한 내용은 [SET ANSI_NULLS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)를 참조하세요.|  
|**ANSI_PADDING**|**boolean**|(선택 사항) 정의된 크기보다 짧은 값을 열에서 저장하는 방법을 제어합니다. 인덱스가 계산 열 또는 뷰에 있는 경우 이 특성을 설정해야 합니다. 예를 들어 다음 구문은 이 특성을 설정합니다.<br /><br /> `<Index ANSI_PADDING [...]>`<br /><br /> 기본적으로 이 특성은 해제되어 있습니다.<br /><br /> 자세한 내용은 [SET ANSI_PADDING&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)을 참조하세요.|  
|**ANSI_WARNINGS**|**boolean**|(선택 사항) 여러 오류 상황에 대한 ISO 표준 동작을 지정합니다. 인덱스가 계산 열 또는 뷰에 있는 경우 이 특성을 설정해야 합니다. 예를 들어 다음 구문은 이 특성을 설정합니다.<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> 기본적으로 이 특성은 해제되어 있습니다.<br /><br /> 자세한 내용은 [SET ANSI_WARNINGS&#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)를 참조하세요.|  
|**NUMERIC_ROUNDABORT**|**boolean**|(선택 사항) 식의 반올림에서 정밀도가 손실될 경우 생성되는 오류 보고의 수준을 지정합니다. 인덱스가 계산 열 또는 뷰에 있는 경우 이 특성을 해제해야 합니다.<br /><br /> 다음 구문은 이 특성을 설정합니다.<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> 기본적으로 이 특성은 해제되어 있습니다.<br /><br /> 자세한 내용은 [SET NUMERIC_ROUNDABORT&#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)를 참조하세요.|  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|**Create** 또는 **Drop** 요소를 사용하여 다른 물리적 디자인 구조를 지정하지 않은 경우 각 **Statistics** 또는 **Heap** 요소에 한 번만 지정해야 합니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Create 요소&#40;DTA&#41;](../../tools/dta/create-element-dta.md)<br /><br /> **Drop** 요소입니다. 자세한 내용은 데이터베이스 엔진 튜닝 관리자 XML 스키마를 참조하십시오.|  
|**자식 요소**|[Index의 Name 요소&#40;DTA&#41;](../../tools/dta/name-element-for-index-dta.md)<br /><br /> [Index의 Column 요소&#40;DTA&#41;](../../tools/dta/column-element-for-index-dta.md)<br /><br /> **PartitionScheme** 요소입니다. 자세한 내용은 데이터베이스 엔진 튜닝 관리자 XML 스키마를 참조하십시오.<br /><br /> **PartitionColumn** 요소입니다. 자세한 내용은 데이터베이스 엔진 튜닝 관리자 XML 스키마를 참조하십시오.<br /><br /> [Index의 Filegroup 요소&#40;DTA&#41;](../../tools/dta/filegroup-element-for-index-dta.md)<br /><br /> **NumberOfReferences** 요소입니다. 자세한 내용은 데이터베이스 엔진 튜닝 관리자 XML 스키마를 참조하십시오.<br /><br /> **PercentUsage** 요소입니다. 자세한 내용은 데이터베이스 엔진 튜닝 관리자 XML 스키마를 참조하십시오.|  
  
## <a name="example"></a>예제  
 이 요소의 사용 예를 보려면 [사용자 정의 구성이 포함된 XML 입력 파일 예제&#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
