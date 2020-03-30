---
title: Excel 사용자 지정 속성 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bdcc72b8-8950-47bd-88bf-5db6d48cc6bf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8ced076a2f8985e1734b36d4795cf81ffe538278
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71292798"
---
# <a name="excel-custom-properties"></a>Excel 사용자 지정 속성

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **원본 사용자 지정 속성**  
  
 Excel 원본에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 Excel 원본의 사용자 지정 속성에 대해 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|정수|데이터베이스에 액세스하는 데 사용되는 모드입니다. 가능한 값은 **행 집합 열기**, **변수를 사용한 행 집합 열기**, **SQL 명령**및 **변수를 사용한 SQL 명령**입니다. 기본값은 **행 집합 열기**입니다.|  
|CommandTimeout|정수|명령이 종료되기 전의 제한 시간(초)입니다.  값 0은 제한 시간이 없음을 나타냅니다.<br /><br /> **참고** 이 속성은 **Excel 원본 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|OpenRowset|String|행 집합을 여는 데 사용되는 데이터베이스 개체의 이름입니다.|  
|OpenRowsetVariable|String|행 집합을 여는 데 사용되는 데이터베이스 개체의 이름이 포함된 변수입니다.|  
|ParameterMapping|String|SQL 명령의 매개 변수에서 변수로의 매핑입니다.|  
|SqlCommand|String|실행할 SQL 명령입니다.|  
|SqlCommandVariable|String|실행할 SQL 명령이 포함된 변수입니다.|  
  
 Excel 원본의 출력 및 출력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Excel Source](../../integration-services/data-flow/excel-source.md)을 참조하세요.  
  
 **대상 사용자 지정 속성**  
  
 Excel 대상에는 사용자 지정 속성과 모든 데이터 흐름 구성 요소에 공통된 속성이 모두 있습니다.  
  
 다음 표에서는 Excel 대상의 사용자 지정 속성을 설명합니다. 모든 속성은 읽기/쓰기가 가능합니다.  
  
|속성 이름|데이터 형식|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer(열거형)|대상에서 해당 대상 데이터베이스에 액세스하는 방법을 지정하는 값입니다.<br /><br /> 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **OpenRowset**(0) - 테이블 또는 뷰의 이름을 제공합니다.<br /><br /> **변수를 사용한 OpenRowset**(1) - 테이블 또는 뷰의 이름이 포함된 변수의 이름을 제공합니다.<br /><br /> **FastLoad를 사용한 OpenRowset**(3) - 테이블 또는 뷰의 이름을 제공합니다.<br /><br /> **변수와 FastLoad를 사용한 OpenRowset**(4) - 테이블 또는 뷰의 이름이 포함된 변수의 이름을 제공합니다.<br /><br /> **SQL 명령**(2) - SQL 문을 제공합니다.|  
|CommandTimeout|정수|제한 시간이 초과될 때까지 SQL 명령을 실행할 수 있는 최대 시간(초)입니다. 값 **0** 은 제한 시간이 없음을 의미합니다. 이 속성의 기본값은 **0**입니다.<br /><br /> 참고: 이 속성은 **Excel 대상 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|FastLoadKeepIdentity|부울|데이터를 로드할 때 ID 값을 복사할지 여부를 지정하는 값입니다. 이 속성은 빠른 로드 옵션 중 하나를 사용할 경우에만 사용할 수 있습니다. 이 속성의 기본값은 **False**입니다.|  
|FastLoadKeepNulls|부울|데이터를 로드할 때 Null 값을 복사할지 여부를 지정하는 값입니다. 이 속성은 빠른 로드 옵션 중 하나와 함께 사용해야 합니다. 이 속성의 기본값은 **False**입니다.|  
|FastLoadMaxInsertCommitSize|정수|Excel 대상에서 빠른 로드 작업을 수행하는 동안 커밋을 시도하는 일괄 처리 크기를 지정하는 값입니다. 기본값은 **2147483647**입니다. **0** 값은 모든 행이 처리된 후의 단일 커밋 작업을 나타냅니다.|  
|FastLoadOptions|String|빠른 로드 옵션 모음입니다. 빠른 로드 옵션에는 테이블 잠금 및 제약 조건 검사가 포함됩니다. 둘 다 또는 둘 중 하나를 지정하거나 아무 것도 지정하지 않을 수 있습니다.<br /><br /> 참고: 이 속성의 일부 옵션은 **Excel 대상 편집기**에서 사용할 수 없지만 **고급 편집기**를 사용하여 설정할 수 있습니다.|  
|OpenRowset|String|AccessMode가 **OpenRowset**인 경우 Excel 대상에서 액세스하는 테이블 또는 뷰의 이름입니다.|  
|OpenRowsetVariable|String|AccessMode가 **변수를 사용한 OpenRowset**인 경우 Excel 대상에서 액세스하는 테이블 또는 뷰의 이름이 포함된 변수의 이름입니다.|  
|SqlCommand|String|AccessMode가 **SQL 명령**인 경우 데이터의 대상 열을 지정하기 위해 Excel 대상에서 사용하는 Transact-SQL 문입니다.|  
  
 Excel 대상의 입력 및 입력 열에는 사용자 지정 속성이 없습니다.  
  
 자세한 내용은 [Excel Destination](../../integration-services/data-flow/excel-destination.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
 [SSIS(SQL Server Integration Services)를 통해 Excel에서 데이터 로드](../load-data-to-from-excel-with-ssis.md)
  
  
