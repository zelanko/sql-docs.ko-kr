---
title: PolyBase의 질문과 대답 | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.openlocfilehash: 9d4cda6dd0fdade80521a801799e5ee53a80c140
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71710549"
---
# <a name="frequently-asked-questions"></a>질문과 대답

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

## <a name="polybase-vs-linked-servers"></a>PolyBase 및 연결된 서버
다음 표에서는 PolyBase와 연결된 서버 기능 간의 차이점을 보여 줍니다.

|PolyBase | 연결된 서버|
|--------------------------|--------------------------|  
|데이터베이스 범위 지정 개체|인스턴스 범위 지정 개체|
|ODBC 드라이버 사용|OLEDB 공급 기업 사용|
|모든 데이터 원본에 대한 읽기 전용 작업과 HADOOP 및 데이터 풀 데이터 원본에 대한 삽입 작업만 지원합니다.|읽기와 쓰기 작업을 모두 지원합니다.|
|단일 연결에서 원격 데이터 원본에 수행하는 쿼리는 확장할 수 있습니다. |단일 연결에서 원격 데이터 원본에 수행하는 쿼리는 확장할 수 없습니다.|
|조건자 푸시 다운이 지원됩니다.|조건자 푸시 다운이 지원됩니다.|
|가용성 그룹에 필요한 별도 구성이 없습니다.|가용성 그룹의 각 인스턴스에 별도 구성이 필요합니다.|
|기본 인증 전용입니다.|기본 및 통합 인증|
|많은 수의 행을 처리하는 분석 쿼리에 적합합니다.|하나 또는 몇개의 행을 반환하는 OLTP 쿼리에 적합합니다.|
|외부 테이블을 사용하는 쿼리는 분산 트랜잭션에 참여할 수 없습니다.|분산 쿼리는 분산 트랜잭션에 참여할 수 있습니다.|

## <a name="whats-new-in-polybase-2019"></a>PolyBase 2019의 새로운 기능 

이제 [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)]의 PolyBase는 다양한 데이터 원본에서 데이터를 읽을 수 있습니다. 이러한 외부 데이터 원본의 데이터는 SQL Server의 외부 테이블인 저장소일 수 있습니다. PolyBase는 ODBC 제네릭 형식을 제외한 이러한 외부 데이터 원본에 대한 푸시다운 계산을 지원합니다.

### <a name="compatible-data-sources"></a>호환 가능한 데이터 원본

- SQL Server
- Oracle
- Teradata
- MongoDB
- 호환 가능한 ODBC 제네릭 형식
  
> [!NOTE]
> PolyBase는 타사 ODBC 드라이버를 사용하여 외부 데이터 원본에 연결할 수 있습니다. 이러한 드라이버는 PolyBase와 함께 제공되지 않으며 의도한 대로 작동하지 않을 수 있습니다. 자세한 내용은 PolyBase ODBC 제네릭 구성에 대한 [가이드](../../relational-databases/polybase/polybase-configure-odbc-generic.md)를 참조하세요.  

## <a name="polybase-in-big-data-clusters-vs-polybase-in-stand-alone-instances"></a>빅 데이터 클러스터의 PolyBase 및 독립 실행형 인스턴스의 PolyBase

다음 표에는 [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] 독립 실행형 설치와 [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] 빅 데이터 클러스터에서 사용할 수 있는 PolyBase 기능이 표시되어 있습니다.

|기능 |빅 데이터 클러스터|독립 실행형 인스턴스|
|--------------------------|--------------------------|---------|   
|SQL Server, Oracle, Teradata 및 Mongo DB를 위한 외부 데이터 원본 만들기 |X|X |
|호환 가능한 타사 ODBC 드라이버를 사용하여 외부 데이터 원본 만들기 | | X|
|HADOOP 데이터 원본용 외부 데이터 원본 만들기 | X| X|
|Azure Blob Storage용 외부 데이터 원본 만들기 | X| X|
|SQL Server 데이터 풀에서 외부 테이블 만들기 | X| |
|SQL Server 스토리지 풀에서 외부 테이블 만들기 | X| |
|쿼리 실행 확장 | X| X|

> [!NOTE]
>최신 [!INCLUDE[sssqlv15](../../includes/sssqlv15-md.md)] CTP에서 사용할 수 있는 기능은 이 표에서 설명하지 않습니다. 사용할 수 있는 기능에 대해서는 릴리스 정보를 참조하세요. ODBC 제네릭 커넥터를 사용하는 연결에 대한 자세한 내용은 [ODBC 제네릭 형식을 구성하는 방법 가이드](polybase-configure-odbc-generic.md)를 참조하세요.