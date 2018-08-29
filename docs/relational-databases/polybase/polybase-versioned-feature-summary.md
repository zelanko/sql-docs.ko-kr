---
title: PolyBase 버전 기능 요약 | Microsoft 문서
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.technology: polybase
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bc95156f93b6b87d317348f56e1b06f57439ada2
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43102111"
---
# <a name="polybase-versioned-feature-summary"></a>PolyBase 버전 기능 요약
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
## <a name="see-also"></a>참고 항목  
 [PolyBase 가이드](../../relational-databases/polybase/polybase-guide.md)  
  
  
