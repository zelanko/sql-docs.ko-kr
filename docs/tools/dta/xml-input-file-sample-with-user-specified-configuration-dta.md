---
title: 사용자 지정 구성이 포함된 XML 입력 파일 샘플(DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: b29c9716-e5c3-4003-9efb-3ade2197b630
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1822e17af7e208cece782e2980a7b9908efe520f
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54255748"
---
# <a name="xml-input-file-sample-with-user-specified-configuration-dta"></a>사용자 지정 구성이 포함된 XML 입력 파일 예제(DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **Configuration** 요소를 사용하여 사용자 지정 구성을 지정하는 이 XML 입력 파일 예제를 복사하여 좋아하는 XML 편집기나 텍스트 편집기에 붙여넣습니다. 이렇게 하면 "가정(what-if)" 분석을 수행할 수 있습니다. "가정(what-if)" 분석에는 **Configuration** 요소를 사용하여 튜닝할 데이터베이스에 대한 가상 실제 디자인 구조 집합을 지정하는 것이 포함됩니다. 그런 다음 데이터베이스 엔진 튜닝 관리자를 사용하여 이 가상 구성에 대해 작업을 실행하는 것의 효과를 분석하여 쿼리 처리 성능을 향상시키는지 여부를 확인합니다. 이 분석 유형은 실제 구현 시 오버헤드를 발생시키지 않고 새 구성을 평가하는 이점이 있습니다. 가상 구성이 원하는 성능 향상을 제공하지 않을 경우 필요한 결과를 달성하는 구성에 도달할 때까지 가상 구성을 쉽게 변경하여 다시 분석할 수 있습니다.  
  
 이 예제를 편집 도구에 복사한 후에 **Server**, **Database**, **Schema**, **Table**, **Workload**, **TuningOptions**및 **Configuration** 요소에 지정된 값을 특정 튜닝 세션에 대한 값으로 바꿉니다. 이러한 요소에 사용할 수 있는 모든 특성 및 자식 요소에 대한 자세한 내용은 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)를 참조하세요. 다음 예에서는 사용 가능한 특성 및 자식 요소 옵션의 하위 집합만 사용합니다.  
  
## <a name="code"></a>코드  
  
```  
<?xml version="1.0" encoding="utf-16" ?>  
<DTAXML xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="https://schemas.microsoft.com/sqlserver/2004/07/dta">  
  <DTAInput>  
    <Server>  
      <Name>MyServerName</Name>  
<!-- To tune multiple databases, list them and their associated tables in the following section. -->  
      <Database>  
        <Name>MyDatabaseName</Name>  
        <Schema>  
          <Name>MyDatabaseSchemaName</Name>  
<!-- You can list as many tables as necessary in the following section. -->  
          <Table>  
            <Name>MyTableName1</Name>  
          </Table>  
          <Table>  
            <Name>MyTableName2</Name>  
          </Table>  
        </Schema>  
      </Database>  
    </Server>  
    <Workload>  
<!-- The following element specifies a workload file, which can be a trace file or a Transact-SQL script file. -->  
      <File>c:\PathToYourWorkloadFile</File>  
    </Workload>  
    <TuningOptions>  
      <TuningTimeInMin>180</TuningTimeInMin>  
      <StorageBoundInMB>10000</StorageBoundInMB>  
      <FeatureSet>IDX_IV</FeatureSet>  
      <Partitioning>NONE</Partitioning>  
      <KeepExisting>NONE</KeepExisting>  
      <OnlineIndexOperation>OFF</OnlineIndexOperation>  
    </TuningOptions>  
    <Configuration SpecificationMode="Absolute">  
      <Server>  
        <Name>MyServerName</Name>  
          <Database>  
            <Name>MyDatabaseName</Name>  
            <Schema>  
              <Name>MyDatabaseSchemaName</Name>  
                <Table>  
                  <Name>MyTableName1</Name>  
                  <Recommendation>  
                    <Create>  
                      <Index Clustered="true" Unique="false" Online="false" IndexSizeInMB="873.75">  
                        <Name>MyIndexName</Name>  
                        <Column Type="KeyColumn" SortOrder="Ascending">  
                          <Name>MyColumnName1</Name>  
                        </Column>  
                        <Filegroup>MyFileGroupName1</FileGroup>  
                      </Index>  
                    </Create>  
                  </Recommendation>  
                </Table>  
            </Schema>  
          </Database>  
      </Server>  
    </Configuration>  
  </DTAInput>  
</DTAXML>  
```  
  
## <a name="comments"></a>주석  
  
-   **Configuration** 요소에 대해 **Absolute** 모드를 지정할 경우(`Configuration SpecificationMode="Absolute"`) 실제 디자인 구조의 삭제는 지원되지 않습니다.  
  
-   **Configuration** 요소의 두 모드( **Relative**또는 **Absolute** )에서 모두 동일한 실제 디자인 구조를 만들고 삭제할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 엔진 튜닝 관리자 시작 및 사용](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [데이터베이스 엔진 튜닝 관리자의 출력 보기 및 작업](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
