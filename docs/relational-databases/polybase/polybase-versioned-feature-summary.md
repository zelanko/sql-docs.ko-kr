---
title: PolyBase 기능 및 제한 사항 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2052b098f0be7ab377cf38a36b896794d3caa07a
ms.sourcegitcommit: 8dccf20d48e8db8fe136c4de6b0a0b408191586b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48874351"
---
# <a name="polybase-features-and-limitations"></a>PolyBase 기능 및 제한 사항

[!INCLUDE[appliesto-ss2016-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

SQL Server 제품 및 서비스에 사용할 수 있는 PolyBase 기능 요약입니다.  
  
## <a name="feature-summary-for-product-releases"></a>제품 릴리스에 대한 기능 요약

이 표에서는 PolyBase 및 이를 사용할 수 있는 제품에 대한 주요 기능을 요약합니다.  
  
||||||
|-|-|-|-|-|   
|**기능**|**SQL Server 2016**|**Azure SQL Database**|**Azure SQL 데이터 웨어하우스**|**병렬 데이터 웨어하우스**| 
|다음을 사용하여 Hadoop 데이터 쿼리 [!INCLUDE[tsql](../../includes/tsql-md.md)]|예|아니요|아니요|예|
|Hadoop에서 데이터 가져오기|예|아니요|아니요|예|
|Hadoop으로 데이터 내보내기  |예|아니요|아니요| 예|
|HDInsight 쿼리, HDInsight에서 가져오기, HDInsight로 내보내기 |아니요|아니요|아니요|아니요
|Hadoop으로 쿼리 계산 푸시다운|예|아니요|아니요|예|  
|Azure Blob 저장소에서 데이터 가져오기|예|아니요|예|예| 
|Azure Blob 저장소로 데이터 내보내기|예|아니요|예|예|  
|Azure Data Lake Store에서 데이터 가져오기|아니요|아니요|예|아니요|    
|Azure Data Lake Store에서 데이터 내보내기|아니요|아니요|예|아니요|
|Microsoft의 BI 도구에서 PolyBase 쿼리 실행|예|아니요|예|예|   

## <a name="pushdown-computation-supported-t-sql-operators"></a>푸시 다운 계산 지원 T-SQL 연산자

SQL Server 및 APS에서 모든 T-SQL 운영자가 hadoop 클러스터로 푸시 다운될 수 있는 것은 아닙니다. 아래 테이블에는 지원되는 모든 운영자와 지원되지 않는 운영자의 하위 집합이 나와 있습니다. 

||||
|-|-|-| 
|**연산자 유형**|**Hadoop으로 푸시 가능**|**Blob Storage로 푸시 가능**|
|열 프로젝션|예|아니요|
|조건자|예|아니요|
|집계|부분|아니요|
|외부 테이블간 조인|아니요|아니요|
|외부 테이블과 로컬 테이블간 조인|아니요|아니요|
|정렬|아니요|아니요|

부분 집계는 데이터가 SQL Server에 도달하면 최종 집계가 발생해야 하지만 집계의 일부가 Hadoop에서 발생하는 것을 의미합니다. 이것은 대량 병렬 처리 시스템에서 집계를 계산하는 일반적인 메서드입니다.  

## <a name="known-limitations"></a>알려진 제한 사항

PolyBase에는 다음과 같은 제한 사항이 있습니다.

- 가변 길이 열의 전체 길이를 포함하여 행의 최대 가능 크기는 SQL Server에서 32KB를 초과하거나, Azure SQL Data Warehouse에서 1MB를 초과할 수 없습니다.

- PolyBase는 Hive 0.12+ 데이터 유형(즉, Char(), VarChar())을 지원하지 않습니다.

- SQL Server 또는 Azure SQL Data Warehouse에서 ORC 파일 형식으로 데이터를 내보낼 때 텍스트가 많은 열은 java 메모리 부족 오류로 인해 50개 이내로 제한될 수 있습니다. 이 문제를 해결하려면 열의 하위 집합만 내보냅니다.

- Hadoop에서 암호화된 미사용 데이터를 읽거나 쓸 수 없습니다. 여기에는 HDFS 암호화 영역 또는 투명 암호화가 포함됩니다.

- KNOX가 활성화되어 있으면 PolyBase가 Hortonworks 인스턴스에 연결할 수 없습니다.

- 트랜잭션이 true인 Hive 테이블을 사용하는 경우 PolyBase는 Hive 테이블의 디렉터리에 있는 데이터에 액세스할 수 없습니다.

<!--SQL Server 2016-->
::: moniker range="= sql-server-2016 || =sqlallproducts-allversions"

- [PolyBase는 SQL Server 2016 장애 조치(Failover) 클러스터에 노드를 추가하는 경우 설치되지 않습니다.](https://support.microsoft.com/en-us/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster)

::: moniker-end
- 통합 인증은 지원되지 않습니다. 지금은 사용자 이름 및 암호만 지원됩니다.  
- 기본적으로 암호화를 사용하도록 설정합니다. 암호화를 사용하지 않도록 설정하려면 ...해야 합니다.
- [형식 매핑 제한 사항](polybase-type-mapping.md)


## <a name="security-and-authentication"></a>보안 및 인증 

## <a name="see-also"></a>참고 항목  

[PolyBase 가이드](../../relational-databases/polybase/polybase-guide.md)  
