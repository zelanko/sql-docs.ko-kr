---
title: "PolyBase 가이드 | Microsoft Docs"
ms.date: "12/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-polybase"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
f1_keywords: 
  - "PolyBase"
  - "PolyBase, guide"
helpviewer_keywords: 
  - "PolyBase"
  - "PolyBase, 개요"
  - "Hadoop 가져오기 ×"
  - "Hadoop 내보내기"
  - "Hadoop 내보내기, PolyBase 개요"
  - "Hadoop 가져오기, PolyBase 개요"
ms.assetid: b42b7d48-328a-4046-abe9-f73fd83212dc
caps.latest.revision: 26
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 24
---
# PolyBase 가이드
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  PolyBase는 SQL Server 내에서 비관계형 및 관계형 데이터에 액세스하고 결합하는 기술입니다.   Hadoop 또는 Azure blob 저장소에서 외부 데이터에 대한 쿼리를 실행할 수 있습니다.   쿼리는 Hadoop에 계산을 푸시하도록 최적화됩니다.  
  
 단순히 Transact-SQL(T-SQL) 문을 사용하여 Hadoop 또는 Azure Blob 저장소에 저장된 비관계형 데이터와 SQL Server의 관계형 테이블 간에 데이터를 가져오고 내보낼 수 있습니다. T-SQL 쿼리 내에서 외부 데이터를 쿼리하고 관계형 데이터를 사용하여 조인할 수도 있습니다.  
  
 PolyBase를 사용하려면 [PolyBase 시작](../../relational-databases/polybase/get-started-with-polybase.md)을 참조하세요.  
  
 ![PolyBase logical](../../relational-databases/polybase/media/polybase-logical.png "PolyBase logical")  
  
## PolyBase를 사용하는 이유는?  
 비즈니스 의사 결정자는 올바른 결정을 위해 관계형 데이터 및 테이블에 구조화되어 있지 않은 기타 데이터(특히 Hadoop 및 기타 NoSQL 기술)를 분석해야 합니다. 다양한 유형의 데이터 저장소 간에 데이터를 전송할 수 있는 방법이 없다면 작업을 수행하는 것이 어렵습니다. PolyBase는 SQL Server의 외부 데이터에 대해 작동하여 이를 수행합니다.  
  
 단순함을 유지하기 위해 PolyBase는 사용자의 Hadoop 또는 Azure 환경에 추가 소프트웨어가 필요하지 않습니다.         외부 데이터 쿼리 작업에는 데이터베이스 테이블 쿼리와 동일한 구문을 사용합니다. 이 작업은 모두 투명하게 수행됩니다. PolyBase는 모든 세부 정보를 백그라운드에서 처리하고 PolyBase를 성공적으로 사용하는 데 Hadoop 또는 Azure에 대해 알 필요가 없습니다.  
  
 PolyBase는 다음 작업을 수행할 수 있습니다.  
  
-   **Hadoop에 저장된 데이터를 쿼리합니다.** 사용자는 Hadoop과 같이 비용 효율적으로 분산되고 확장 가능한 시스템에 데이터 집합을 저장하고 있습니다. PolyBase를 사용하면 쉽게 T-SQL을 사용하여 데이터를 쿼리할 수 있습니다.  
  
-   **Azure blob 저장소에 저장된 데이터를 쿼리합니다.** Azure blob 저장소는 Azure 서비스에서 사용 하기 위해 데이터를 저장하는 편리한 장소입니다.  PolyBase는 T-SQL을 사용하여 쉽게 데이터에 액세스할 수 있습니다.  
  
-   **Hadoop 또는 Azure blob 저장소에서 데이터를 가져옵니다.** Microsoft SQL columnstore 기술 및 분석 기능의 속도를 활용하여 Hadoop 또는 Azure blob 저장소에서 관계형 테이블에 데이터를 가져옵니다. 별도 ETL 또는 가져오기 도구에 대한 요구 사항이 없습니다.  
  
-   **Hadoop 또는 Azure Blob 저장소로 데이터 내보내기.** Hadoop 또는 Azure blob 저장소에 데이터를 보관하여 비용 효율적인 저장소를 구현하고 손쉽게 액세스할 수 있도록 온라인 상태로 유지합니다.  
  
-   **BI 도구와 통합.** PolyBase는 Microsoft의 비즈니스 인텔리전스 및 분석 스택에서 사용하거나 SQL Server와 호환되는 타사 도구를 사용합니다.  
  
## 성능  
  
-   **Hadoop에 계산 푸시.**쿼리 최적화 프로그램은 비용 기반 결정을 내려 Hadoop에 계산을 푸시하며 이를 통해 쿼리 성능이 향상됩니다.  외부 테이블의 통계를 사용하여 비용 기반 결정을 내립니다.   계산을 푸시하는 데는 MapReduce 작업을 만들고 Hadoop의 분산된 계산 리소스를 활용합니다.  
  
-   **계산 리소스 크기 조정.** 쿼리 성능을 향상시키기 위해 SQL Server [PolyBase 확장 그룹](../../relational-databases/polybase/polybase-scale-out-groups.md)을 사용할 수 있습니다. 이를 통해 Hadoop 노드와 SQL Server 인스턴스 간에 병렬 데이터 전송이 가능하며 외부 데이터에서 작동하기 위한 계산 리소스를 추가합니다.  
  
## PolyBase 가이드 항목  
 이 가이드에는 효율적이고 효과적으로 PolyBase를 사용하는 항목이 포함되어 있습니다.  
  
|||  
|-|-|  
|**항목**|**설명**|  
|[PolyBase 시작하기](../../relational-databases/polybase/get-started-with-polybase.md)|PolyBase를 설치하고 구성하는 기본 단계입니다. Hadoop 또는 Azure blob 저장소의 데이터를 가리키는 외부 개체를 만드는 방법을 보여 주며 쿼리 예제를 제공합니다.|  
|[PolyBase 버전 기능 요약](../../relational-databases/polybase/polybase-versioned-feature-summary.md)|SQL Server, SQL 데이터베이스 및 SQL 데이터 웨어하우스에서 지원되는 PolyBase 기능을 설명합니다.|  
|[PolyBase 확장 그룹](../../relational-databases/polybase/polybase-scale-out-groups.md)|SQL Server 확장 그룹을 사용하여 SQL Server 및 Hadoop 간에 병렬 처리를 확장합니다.|  
|[PolyBase 설치](../../relational-databases/polybase/polybase-installation.md)|설치 마법사 또는 명령줄 도구를 사용하여 PolyBase를 설치하기 위한 단계 및 참조 사항입니다.|  
|[PolyBase 구성](../../relational-databases/polybase/polybase-configuration.md)|PolyBase용 SQL Server 설정을 구성합니다.  예를 들어 계산 푸시다운 및 kerberos 보안을 구성합니다.|  
|[PolyBase T-SQL 개체](../../relational-databases/polybase/polybase-t-sql-objects.md)|PolyBase가 외부 데이터를 정의하고 액세스하는 데 사용하는 T-SQL 개체를 만듭니다.|  
|[PolyBase Queries](../../relational-databases/polybase/polybase-queries.md)|T-SQL 문을 사용하여 외부 데이터를 쿼리, 가져오기 또는 내보냅니다.|  
|[PolyBase 문제 해결](../../relational-databases/polybase/polybase-troubleshooting.md)|PolyBase 쿼리를 관리하는 기술입니다. DMV(동적 관리 뷰)를 사용하여 PolyBase 쿼리를 모니터링하고 PolyBase 쿼리 계획을 확인하여 성능 병목 현상을 찾아내는 방법을 알아봅니다.|  
  
  