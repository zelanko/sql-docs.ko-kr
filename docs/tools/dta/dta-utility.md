---
title: "dta 유틸리티 | Microsoft Docs"
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- physical design structures [SQL Server]
- command prompt utilities [SQL Server], dta
- dta utility
- tuning databases [SQL Server], Database Engine Tuning Advisor
- workloads [SQL Server], analyzing
- dta utility, about dta utility
- performance [SQL Server], Database Engine Tuning Advisor
- Database Engine Tuning Advisor [SQL Server], command prompt
- optimizing databases [SQL Server]
ms.assetid: a0b210ce-9b58-4709-80cb-9363b68a1f5a
caps.latest.revision: 58
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 5e364743bf03da5f76b776174241bf3911a6b447
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="dta-utility"></a>dta 유틸리티
  **dta** 유틸리티는 데이터베이스 엔진 튜닝 관리자의 명령 프롬프트 버전입니다. **dta** 유틸리티를 통해 응용 프로그램과 스크립트에서 데이터베이스 엔진 튜닝 관리자의 기능을 사용할 수 있습니다.  
  
 데이터베이스 엔진 튜닝 관리자와 마찬가지로 **dta** 유틸리티는 작업을 분석하고 이 작업에 대해 서버 성능을 향상시키기 위한 물리적 디자인 구조를 제안합니다. 작업은 계획 캐시, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 추적 파일이나 테이블 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트일 수 있습니다. 물리적 디자인 구조에는 인덱스, 인덱싱된 뷰 및 분할이 포함됩니다. 작업을 분석한 후 **dta** 유틸리티는 실제 데이터베이스 디자인을 제안하며 이 제안 사항을 구현하는 데 필요한 스크립트를 생성할 수 있습니다. 명령 프롬프트에서 **-if** 또는 **-it** 인수를 사용하여 작업을 지정할 수 있습니다. 또한 명령 프롬프트에서 **-ix** 인수를 사용하여 XML 입력 파일을 지정할 수도 있습니다. 이러한 경우 작업은 XML 입력 파일에서 지정됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
dta  
[ -? ] |  
[  
      [ -S server_name[ \instance ] ]  
      { { -U login_id [-P password ] } | –E  }  
      { -D database_name [ ,...n ] }  
      [ -d database_name ]   
      [ -Tl table_list | -Tf table_list_file ]  
      { -if workload_file | -it workload_trace_table_name  |   
        -ip | -iq }  
      { -ssession_name | -IDsession_ID }  
      [ -F ]  
      [ -of output_script_file_name ]  
      [ -or output_xml_report_file_name ]  
      [ -ox output_XML_file_name ]  
      [ -rl analysis_report_list [ ,...n ] ]  
      [ -ix input_XML_file_name ]  
      [ -A time_for_tuning_in_minutes ]  
      [ -n number_of_events ]
      [ -I time_window_in_hours ]  
      [ -m minimum_improvement ]  
      [ -fa physical_design_structures_to_add ]  
      [ -fi filtered_indexes]  
      [ -fc columnstore_indexes]  
      [ -fp partitioning_strategy ]  
      [ -fk keep_existing_option ]  
      [ -fx drop_only_mode ]  
      [ -B storage_size ]  
      [ -c max_key_columns_in_index ]  
      [ -C max_columns_in_index ]  
      [ -e | -e tuning_log_name ]  
      [ -N online_option]  
      [ -q ]  
      [ -u ]  
      [ -x ]  
      [ -a ]  
]  
```  
  
## <a name="arguments"></a>인수  
 **-?**  
 사용법 정보를 표시합니다.  
  
 **-A** *time_for_tuning_in_minutes*  
 튜닝 시간 제한(분)을 지정합니다. **dta** 는 지정된 시간 동안 작업을 튜닝하고 제안된 실제 디자인 변경 내용을 사용하여 스크립트를 생성합니다. **dta** 의 기본 튜닝 시간은 8시간입니다. 0을 지정하면 튜닝에 시간 제한이 없습니다. **dta** 는 시간 제한이 만료되기 전에 전체 작업 튜닝을 마칠 수 있습니다. 그러나 전체 작업이 튜닝되도록 하려면 무제한 튜닝 시간(-A 0)을 지정하는 것이 좋습니다.  
  
 **-a**  
 작업을 튜닝한 후 사용자에게 메시지를 표시하지 않고 제안 사항을 적용합니다.  
  
 **-B** *storage_size*  
 권장되는 인덱스 및 분할에서 소비할 수 있는 최대 공간(MB)을 지정합니다. 여러 개의 데이터베이스를 튜닝할 경우 모든 데이터베이스에 대한 권장 구성은 공간 계산을 고려하여 처리됩니다. 기본적으로 **dta** 는 다음 저장소 크기 중 더 작은 크기를 사용합니다.  
  
-   현재 원시 데이터 크기의 3배이며 데이터베이스의 테이블에 있는 힙과 클러스터형 인덱스의 전체 크기를 포함합니다.  
  
-   연결된 모든 디스크 드라이브의 여유 공간과 원시 데이터 크기를 더한 것입니다.  
  
 기본 저장소 크기는 비클러스터형 인덱스 및 인덱싱된 뷰를 포함하지 않습니다.  
  
 **-C** *max_columns_in_index*  
 **dta** 에서 제안하는 인덱스의 최대 열 수를 지정합니다. 최대값은 1024입니다. 기본적으로 이 인수는 16으로 설정됩니다.  
  
 **-c** *max_key_columns_in_index*  
 **dta** 에서 제안하는 인덱스의 최대 키 열 수를 지정합니다. 기본값은 16이며 허용되는 최대값입니다. **dta** 는 포함된 열을 사용하여 인덱스를 만듭니다. 포함된 열을 사용할 때 권장되는 인덱스는 이 인수에 지정된 열 수를 초과할 수 있습니다.  
  
 **-D** *database_name*  
 튜닝할 각 데이터베이스의 이름을 지정합니다. 첫 번째 데이터베이스가 기본 데이터베이스입니다. 다음과 같이 데이터베이스 이름을 쉼표로 구분하여 여러 데이터베이스를 지정할 수 있습니다.  
  
```  
dta –D database_name1, database_name2...  
```  
  
 또는 다음과 같이 각 데이터베이스 이름에 **–D** 인수를 사용하여 여러 데이터베이스를 지정할 수 있습니다.  
  
```  
dta –D database_name1 -D database_name2... n  
```  
  
 **-D** 인수는 필수 인수입니다. **-d** 인수를 지정하지 않은 경우 초기에 **dta** 는 작업에서 첫 번째 `USE database_name` 절로 지정된 데이터베이스에 연결합니다. 작업에 명시적 `USE database_name` 절이 없으면 **-d** 인수를 사용해야 합니다.  
  
 예를 들어 작업에 명시적 `USE database_name` 절이 포함되지 않은 경우 다음 **dta** 명령을 사용하면 권장 구성이 생성되지 않습니다.  
  
```  
dta -D db_name1, db_name2...  
```  
  
 그러나 같은 작업에서 **-d** 인수를 사용하는 다음 **dta** 명령을 사용하면 권장 구성이 생성됩니다.  
  
```  
dta -D db_name1, db_name2 -d db_name1  
```  
  
 **-d** *database_name*  
 작업을 튜닝할 때 **dta** 가 연결하는 첫 번째 데이터베이스를 지정합니다. 이 인수에는 데이터베이스를 하나만 지정할 수 있습니다. 예를 들어  
  
```  
dta -d AdventureWorks2012 ...  
```  
  
 데이터베이스 이름을 여러 개 지정할 경우 **dta** 는 오류를 반환합니다. **-d** 인수는 선택 사항입니다.  
  
 XML 입력 파일을 사용하는 경우 **DatabaseToConnect** 요소 아래에 있는 **TuningOptions** 요소를 사용하여 **dta** 가 연결하는 첫 번째 데이터베이스를 지정할 수 있습니다. 자세한 내용은 [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)을(를) 참조하세요.  
  
 데이터베이스를 하나만 튜닝하는 경우 **-d** 인수는 **sqlcmd** 유틸리티의 **-d** 인수와 유사한 기능을 제공하지만 USE *database_name* 문을 실행하지는 않습니다. 자세한 내용은 [sqlcmd Utility](../../tools/sqlcmd-utility.md)을(를) 참조하십시오.  
  
 **-E**  
 암호를 요구하지 않고 트러스트된 연결을 사용합니다. 로그인 ID를 지정하는 **-E** 인수 또는 **-U** 인수를 사용해야 합니다.  
  
 **-e** *tuning_log_name*  
 **dta** 가 튜닝할 수 없는 이벤트를 기록하는 테이블 또는 파일의 이름을 지정합니다. 이 테이블은 튜닝을 수행하는 서버에 생성됩니다.  
  
 테이블을 사용하는 경우 *[database_name].[owner_name].table_name*형식으로 해당 이름을 지정합니다. 다음 표에서는 각 매개 변수의 기본값을 보여 줍니다.  
  
|매개 변수|기본값|세부 정보|  
|---------------|-------------------|-------------|  
|*database_name*|*–D* 옵션으로 지정된 **database_name**||  
|*owner_name*|**dbo**|*owner_name* 은 **dbo**여야 합니다. 다른 값을 지정할 경우 **dta** 를 실행할 수 없으며 오류가 반환됩니다.|  
|*table_name*|없음||  
  
 파일을 사용하는 경우 TuningLog.xml과 같이 확장명으로 .xml을 지정합니다.  
  
> [!NOTE]  
>  **dta** 유틸리티는 세션을 삭제해도 사용자 지정 튜닝 로그 테이블의 내용을 삭제하지 않습니다. 매우 큰 작업을 튜닝하는 경우 튜닝 로그에 대해 테이블을 지정하는 것이 좋습니다. 큰 작업을 튜닝하면 큰 튜닝 로그가 생성되기 때문에 테이블을 사용하면 세션을 보다 빨리 삭제할 수 있습니다.  
  
 **-F**  
 **dta** 가 기존의 출력 파일을 덮어쓰도록 허용합니다. 이름이 같은 출력 파일이 이미 있을 경우 **-F** 를 지정하지 않으면 **dta**는 오류를 반환합니다. **-of** , **-or**또는 **-ox**와 함께 **-F**를 사용할 수 있습니다.  
  
 **-fa** *physical_design_structures_to_add*  
 **dta** 가 권장 구성에 포함해야 할 실제 디자인 구조 유형을 지정합니다. 다음 표에서는 이 인수에 지정할 수 있는 값을 나열하고 설명합니다. 값을 지정하지 않으면 **dta** 는 기본적으로 **-fa****IDX**를 사용합니다.  
  
|값|설명|  
|-----------|-----------------|  
|IDX_IV|인덱스와 인덱싱된 뷰|  
|IDX|인덱스만|  
|IV|인덱싱된 뷰만|  
|NCL_IDX|비클러스터형 인덱스만|  
  
 **-fi**  
 필터링된 인덱스가 새 제안 사항을 만들 때 고려되도록 지정합니다. 자세한 내용은 [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)을(를) 참조하세요.  
  
**-fc**  
 Columnstore 인덱스를 새 권장 사항에 대 한 고려 지정 합니다. DTA는 모두 클러스터형 및 비클러스터형 columnstore 인덱스를 고려 합니다. 자세한 내용은 다음을 참조하세요.    
[Columnstore 인덱스 권장 구성에서 데이터베이스 엔진 튜닝 관리자 (DTA)](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)합니다.
 ||  
|-|  
|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  

  
 **-fk** *keep_existing_option*  
 권장 구성을 생성할 때 **dta** 가 유지해야 할 기존의 실제 디자인 구조를 지정합니다. 다음 표에서는 이 인수에 지정할 수 있는 값을 나열하고 설명합니다.  
  
|값|설명|  
|-----------|-----------------|  
|없음|기존 구조 없음|  
|ALL|기존의 모든 구조|  
|ALIGNED|모든 파티션 정렬 구조|  
|CL_IDX|테이블에 있는 모든 클러스터형 인덱스|  
|IDX|테이블에 있는 모든 클러스터형 및 비클러스터형 인덱스|  
  
 **-fp** *partitioning_strategy*  
 **dta** 가 제안하는 새 실제 디자인 구조(인덱스 및 인덱싱된 뷰)를 분할할 것인지 여부와 분할 방법을 지정합니다. 다음 표에서는 이 인수에 지정할 수 있는 값을 나열하고 설명합니다.  
  
|값|설명|  
|-----------|-----------------|  
|없음|분할 안 함|  
|FULL|전체 분할(성능 향상 중심)|  
|ALIGNED|정렬된 분할만(관리 효율성 향상 중심)|  
  
 ALIGNED는 **dta** 로 생성된 권장 구성에서 제안된 모든 인덱스가 이 인덱스를 정의한 기본 테이블과 정확히 같은 방식으로 분할됨을 의미합니다. 인덱싱된 뷰의 비클러스터형 인덱스는 인덱싱된 뷰에 정렬됩니다. 이 인수에는 값을 하나만 지정할 수 있습니다. 기본값은 **-fp****NONE**입니다.  
  
 **-fx** *drop_only_mode*  
 **dta** 에서 기존의 실제 디자인 구조의 삭제만 고려할 것인지 지정합니다. 새 물리적 디자인 구조는 고려되지 않습니다. 이 옵션을 지정하면 **dta** 는 기존 물리적 디자인 구조의 유용성을 평가하고 거의 사용하지 않는 구조를 삭제할 것을 권장합니다. 이 인수에는 값이 없습니다. 이 인수는 **-fa**, **-fp**또는 **-fk ALL** 인수와 함께 사용할 수 없습니다.  
  
 **-ID** *session_ID*  
 튜닝 세션에 대한 숫자 식별자를 지정합니다. 이 옵션을 지정하지 않으면 **dta** 는 ID 번호를 생성합니다. 이 식별자를 사용하여 기존 튜닝 세션에 대한 정보를 볼 수 있습니다. **-ID**값을 지정하지 않을 경우 **-s**를 사용하여 세션 이름을 지정해야 합니다.  
  
 **-ip**  
 계획 캐시를 작업으로 사용할 수 있도록 지정합니다. 명시적으로 선택한 데이터베이스에 대한 상위 1,000개의 계획 캐시 이벤트가 분석됩니다. **–n** 옵션을 사용하여 이 값을 변경할 수 있습니다.  
 
**-iq**  
 쿼리 저장소 작업으로 사용할 수 있도록 지정 합니다. 명시적으로 선택한 데이터베이스에 대 한 쿼리 저장소에서 상위 1, 000 이벤트가 분석 됩니다. **–n** 옵션을 사용하여 이 값을 변경할 수 있습니다.  참조 [쿼리 저장소](../../relational-databases/performance/how-query-store-collects-data.md) 및 [쿼리 저장소에서 데이터베이스를 사용 하 여 작업 튜닝](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md) 자세한 정보에 대 한 합니다.
 ||  
|-|  
|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  
     
  
 **-if** *workload_file*  
 튜닝을 위한 입력으로 사용할 작업 파일의 경로와 이름을 지정합니다. 파일은 .trc(SQL Server Profiler 추적 파일), .sql(SQL 파일) 또는 .log([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 추적 파일) 형식 중 하나여야 합니다. 작업 파일 또는 작업 테이블을 하나 지정해야 합니다.  
  
 **-it** *workload_trace_table_name*  
 튜닝을 위한 작업 추적을 포함하는 테이블의 이름을 지정합니다. 이름은 [*database_name*]**.**[*owner_name*]**.***table_name*형식으로 지정됩니다.  
  
 다음 표에서는 각 매개 변수의 기본값을 보여 줍니다.  
  
|매개 변수|기본값|  
|---------------|-------------------|  
|*database_name*|*–D* 옵션으로 지정된 **database_name**|  
|*owner_name*|**dbo**|  
|*table_name*|없음|  
  
> [!NOTE]  
>  *owner_name*은 **dbo**여야 합니다. 다른 값을 지정하면 **dta** 가 실행되지 않고 오류가 반환됩니다. 작업 파일 또는 작업 테이블 하나를 지정해야 합니다.  
  
 **-ix** *input_XML_file_name*  
 **dta** 입력 정보가 포함된 XML 파일의 이름을 지정합니다. 이 파일은 DTASchema.xsd를 준수하는 유효한 XML 문서여야 합니다. 명령 프롬프트에서 튜닝 옵션에 대해 지정한 인수와 충돌하면 이 XML 파일의 해당 값보다 우선 적용됩니다. 단, 사용자 지정 구성을 XML 입력 파일에 평가 모드로 입력할 경우는 예외입니다. 예를 들어 XML 입력 파일의 **Configuration** 요소에 구성을 입력하고 튜닝 옵션 중 하나로 **EvaluateConfiguration** 요소를 지정한 경우 XML 입력 파일에서 지정한 튜닝 옵션은 명령 프롬프트에서 입력한 튜닝 옵션보다 우선 적용됩니다.  
  
 **-m** *minimum_improvement*  
 권장 구성이 만족시켜야 할 최소 향상률을 지정합니다.  
  
 **-N** *online_option*  
 물리적 디자인 구조를 온라인으로 만들 것인지 여부를 지정합니다. 다음 표에서는 이 인수에 지정할 수 있는 값을 나열하고 설명합니다.  
  
|값|설명|  
|-----------|-----------------|  
|OFF|권장되는 물리적 디자인 구조를 온라인으로 만들 수 없습니다.|  
|ON|권장되는 모든 물리적 디자인 구조를 온라인으로 만들 수 있습니다.|  
|MIXED|데이터베이스 엔진 튜닝 관리자는 가능한 경우 온라인으로 만들 수 있는 물리적 디자인 구조를 제안합니다.|  
  
 인덱스를 온라인으로 만드는 경우 개체 정의에 ONLINE = ON이 추가됩니다.  
  
 **-n** *number_of_events*  
 **dta** 가 튜닝해야 할 작업의 이벤트 수를 지정합니다. 이 인수를 지정한 경우 작업이 기간 정보가 포함된 추적 파일이면 **dta** 는 기간의 내림차순으로 이벤트를 튜닝합니다. 이 인수는 물리적 디자인 구조의 두 구성을 비교할 때 유용합니다. 두 구성을 비교하려면 다음과 같이 두 구성에 대해 튜닝할 이벤트 수를 같은 값으로 지정하고 무제한 튜닝 시간을 지정합니다.  
  
```  
dta -n number_of_events -A 0  
```  
  
 이러한 경우 반드시 무제한 튜닝 시간(`-A 0`)을 지정해야 합니다. 그렇지 않으면 기본적으로 데이터베이스 엔진 튜닝 관리자에서 튜닝 시간으로 8시간을 적용합니다.
 
 **-I** *time_window_in_hours*   
   시간 창 (시간)을 지정 DTA 사용 하는 경우 튜닝에 대 한 것으로 간주 되려면에 대 한 쿼리 실행 해야 경우 **-iq** 옵션 (쿼리 저장소에서 작업). 
```  
dta -iq -I 48  
```  
이 경우 DTA 작업의 원본으로 쿼리 저장소를 사용 하 고만 지난 48 시간으로 실행 된 쿼리를 고려 합니다.  
  ||  
|-|  
|**적용 대상**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 부터 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]까지|  


  
 **-or** *output_script_file_name*  
 **dta** 가 권장 구성을 지정된 파일 이름 및 대상에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트로 쓰도록 지정합니다.  
  
 이 옵션과 함께 **-F** 를 사용할 수 있습니다. 파일 이름이 고유한지 확인합니다. 특히 **-or** 및 **-ox**를 함께 사용하는 경우 고유한 파일 이름이어야 합니다.  
  
 **-ox** *output_xml_report_file_name*  
 **dta** 가 권장 구성을 XML 형식의 출력 보고서로 쓰도록 지정합니다. 파일 이름을 제공한 경우 권장 구성이 해당 대상에 기록됩니다. 그렇지 않으면 **dta** 는 세션 이름을 사용하여 파일 이름을 생성하고 현재 디렉터리에 씁니다.  
  
 이 옵션과 함께 **-F** 를 사용할 수 있습니다. 파일 이름이 고유한지 확인합니다. 특히 **-of** 및 **-ox**를 함께 사용하는 경우 고유한 파일 이름이어야 합니다.  
  
 **-F** *output_XML_file_name*  
 **dta** 가 권장 구성을 제공된 파일 이름 및 대상에 XML 파일로 쓰도록 지정합니다. 데이터베이스 엔진 튜닝 관리자에서 대상 디렉터리에 쓸 수 있는 권한이 있는지 확인합니다.  
  
 이 옵션과 함께 **-F** 를 사용할 수 있습니다. 파일 이름이 고유한지 확인합니다. 특히 **-of** 및 **-or**을 함께 사용하는 경우 고유한 파일 이름이어야 합니다.  
  
 **-P** *password*  
 로그인 ID의 암호를 지정합니다. 이 옵션을 사용하지 않으면 **dta** 가 암호를 묻는 메시지를 표시합니다.  
  
 **-q**  
 자동 모드를 설정합니다. 진행률 및 머리글 정보를 포함하여 어떤 정보도 콘솔에 표시되지 않습니다.  
  
 **-rl** *analysis_report_list*  
 생성할 분석 보고서의 목록을 지정합니다. 다음 표에서는 이 인수에 지정할 수 있는 값을 나열합니다.  
  
|값|보고서|  
|-----------|------------|  
|ALL|모든 분석 보고서|  
|STMT_COST|문 비용 보고서|  
|EVT_FREQ|이벤트 빈도 보고서|  
|STMT_DET|문 세부 정보 보고서|  
|CUR_STMT_IDX|문-인덱스 관계 보고서(현재 구성)|  
|REC_STMT_IDX|문-인덱스 관계 보고서(권장 구성)|  
|STMT_COSTRANGE|문 비용 범위 보고서|  
|CUR_IDX_USAGE|인덱스 사용 보고서(현재 구성)|  
|REC_IDX_USAGE|인덱스 사용 보고서(권장 구성)|  
|CUR_IDX_DET|인덱스 세부 정보 보고서(현재 구성)|  
|REC_IDX_DET|인덱스 세부 정보 보고서(권장 구성)|  
|VIW_TAB|뷰-테이블 관계 보고서|  
|WKLD_ANL|작업 분석 보고서|  
|DB_ACCESS|데이터베이스 액세스 보고서|  
|TAB_ACCESS|테이블 액세스 보고서|  
|COL_ACCESS|열 액세스 보고서|  
  
 보고서가 여러 개인 경우 다음과 같이 쉼표로 값을 구분하여 지정합니다.  
  
```  
... -rl EVT_FREQ, VIW_TAB, WKLD_ANL ...  
```  
  
 **-S** *server_name*[ *\instance*]  
 연결할 컴퓨터 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정합니다. *server_name* 을 지정하지 않으면 **dta** 가 로컬 컴퓨터에 있는 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다. 명명된 인스턴스에 연결할 때 또는 네트워크의 원격 컴퓨터에서 **dta** 를 실행할 때 이 옵션을 지정해야 합니다.  
  
 **-s** *session_name*  
 튜닝 세션 이름을 지정합니다. **-ID** 를 지정하지 않는 경우 이 인수를 반드시 지정해야 합니다.  
  
 **-Tf** *table_list_file*  
 튜닝할 테이블 목록이 들어 있는 파일의 이름을 지정합니다. 파일 내에 표시된 각 테이블은 새 줄로 시작해야 합니다. 테이블 이름은 **AdventureWorks2012.HumanResources.Department**와 같이 세 부분으로 이루어진 정규화된 이름이어야 합니다. 또한 테이블 배율 기능을 호출하려면 기존 테이블 이름 뒤에 테이블의 예상 행 수를 나타내는 숫자를 붙일 수 있습니다. 데이터베이스 엔진 튜닝 관리자에서는 이 테이블을 참조하는 작업에서 문을 튜닝하거나 평가하는 동안 예상 행 수를 고려합니다. *number_of_rows* 개수와 *table_name*사이에 하나 이상의 공백이 있을 수 있습니다.  
  
 다음은 *table_list_file*의 파일 형식입니다.  
  
 *database_name*.[*schema_name*].*table_name* [*number_of_rows*]  
  
 *database_name*.[*schema_name*].*table_name* [*number_of_rows*]  
  
 *database_name*.[*schema_name*].*table_name* [*number_of_rows*]  
  
 이 인수는 명령 프롬프트에서 테이블 목록(**-Tl**)을 입력하는 대신 사용할 수 있습니다. **-Tl**를 사용하는 경우 테이블 목록 파일( **-Tf**)을 사용하지 마세요. 두 인수를 모두 사용하면 **dta** 가 실패하고 오류가 반환됩니다.  
  
 **-Tf** 및 **-Tl** 인수를 둘 다 생략하면 지정한 데이터베이스의 모든 사용자 테이블이 튜닝 대상으로 고려됩니다.  
  
 **-Tl** *table_list*  
 명령 프롬프트에서 튜닝할 테이블 목록을 지정합니다. 테이블 이름은 쉼표를 입력하여 구분합니다. **-D** 인수로 데이터베이스를 하나만 지정하는 경우 데이터베이스 이름으로 테이블 이름을 정규화할 필요가 없습니다. 그렇지 않고 여러 데이터베이스를 지정하는 경우에는 각 테이블에 *database_name.schema_name.table_name* 형식으로 정규화된 이름을 사용해야 합니다.  
  
 이 인수는 테이블 목록 파일(**-Tf**) 대신 사용할 수 있습니다. **-Tl** 및 **-Tf** 를 모두 사용하면 **dta** 가 실패하고 오류가 반환됩니다.  
  
 **-U** *login_id*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결에 사용하는 로그인 ID를 지정합니다.  
  
 **-u**  
 데이터베이스 엔진 튜닝 관리자 GUI를 시작합니다. 모든 매개 변수는 사용자 인터페이스의 초기 설정으로 간주됩니다.  
  
 **-x**  
 튜닝 세션을 시작하고 종료합니다.  
  
## <a name="remarks"></a>주의  
 Ctrl+C를 한 번 누르면 튜닝 세션이 중지되고 이 지점까지 **dta** 가 완료한 분석을 기반으로 권장 구성이 생성됩니다. 권장 구성을 생성할지 여부를 결정하라는 메시지가 표시됩니다. Ctrl+C를 다시 누르면 권장 구성을 생성하지 않고 튜닝 세션이 중지됩니다.  
  
## <a name="examples"></a>예  
 **A. 권장 구성에 인덱스 및 인덱싱된 뷰가 포함 된 작업 튜닝**  
  
 이 예에서는 보안 연결(`-E`)을 통해 MyServer에 있는 **tpcd1G** 데이터베이스에 연결하여 작업을 분석하고 권장 구성을 만듭니다. 그리고 script.sql이라는 스크립트 파일에 출력 파일을 씁니다. script.sql이 이미 있을 경우 **인수를 지정했으므로** dta `-F` 는 이 파일을 덮어씁니다. 작업 분석이 완료될 때까지 제한 시간 없이(`-A 0`) 튜닝 세션이 실행됩니다. 권장 구성에서는 최소 향상률 값으로 5%(`-m 5`)를 지정해야 합니다. **dta** 는 최종 권장 구성(`-fa IDX_IV`)에 인덱스 및 인덱싱된 뷰를 포함합니다.  
  
```  
dta –S MyServer –E -D tpcd1G -if tpcd_22.sql -F –of script.sql –A 0 -m 5 -fa IDX_IV  
```  
  
 **B. 디스크 사용 제한**  
  
 이 예에서는 원시 데이터 및 추가 인덱스를 포함하여 총 데이터베이스 크기를 3GB(`-B 3000`)로 제한하고 출력을 d:\result_dir\script1.sql로 보냅니다. 1시간(`-A 60`) 동안만 실행됩니다.  
  
```  
dta –D tpcd1G –if tpcd_22.sql -B 3000 –of "d:\result_dir\script1.sql" –A 60  
```  
  
 **C. 튜닝된 쿼리 수 제한**  
  
 이 예에서는 orders_wkld.sql 파일에서 읽혀지는 최대 쿼리 수를 10(`-n 10`)개로 제한하고 15분(`-A 15`) 동안 실행합니다. 최대 쿼리 10개에 도달하거나 15분이 되면 종료됩니다. 10개 쿼리를 모두 튜닝하려면 `-A 0`을 사용하여 튜닝 시간을 무제한으로 지정합니다. 시간이 중요할 경우 다음 예와 같이 `-A` 인수로 튜닝할 수 있는 시간(분)을 지정하여 적절한 제한 시간을 설정합니다.  
  
```  
dta –D orders –if orders_wkld.sql –of script.sql –A 15 -n 10  
```  
  
 **D. 파일에 나열 된 특정 테이블 튜닝**  
  
 이 예에서는 *table_list_file* ( **-Tf** 인수)을 사용하는 방법을 보여 줍니다. table_list.txt 파일 내용은 다음과 같습니다.  
  
```  
AdventureWorks2012.Sales.Customer  100000  
AdventureWorks2012.Sales.Store  
AdventureWorks2012.Production.Product  2000000  
```  
  
 table_list.txt의 내용은 다음을 지정합니다.  
  
-   데이터베이스에서 **Customer**, **Store**및 **Product** 테이블만 튜닝해야 합니다.  
  
-   **Customer** 및 **Product** 테이블의 행 수는 각각 100,000개와 2,000,000개로 가정됩니다.  
  
-   **Store** 의 행 수는 테이블에 있는 현재 행 수로 가정됩니다.  
  
 *table_list_file*에서 행 개수와 앞 테이블 이름 사이에 하나 이상의 공백이 있을 수 있습니다.  
  
 튜닝 시간은 2시간(`-A 120`)이며 출력은 XML 파일(`-ox XMLTune.xml`)에 기록됩니다.  
  
```  
dta –D pubs –if pubs_wkld.sql –ox XMLTune.xml –A 120 –Tf table_list.txt  
```  
  
## <a name="see-also"></a>참고 항목  
 [명령 프롬프트 유틸리티 참조&#40;데이터베이스 엔진#41;](../../tools/command-prompt-utility-reference-database-engine.md)   
 [데이터베이스 엔진 튜닝 관리자](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  

