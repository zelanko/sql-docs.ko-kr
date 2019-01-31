---
title: PolyBase의 질문과 대답 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: ''
ms.openlocfilehash: 331ac177831b1e07cfab253c363a35f2bab42a6c
ms.sourcegitcommit: ee76381cfb1c16e0a063315c9c7005f10e98cfe6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/26/2019
ms.locfileid: "55072885"
---
# <a name="frequently-asked-questions"></a>질문과 대답

## <a name="polybase-in-big-data-clusters-vs-polybase-in-stand-alone-instances"></a>빅 데이터 클러스터의 PolyBase 및 독립 실행형 인스턴스의 PolyBase

|기능 |빅 데이터 클러스터| 독립 실행형 인스턴스|
|--------------------------|--------------------------|---------|   
|외부 테이블 만들기| X| X|
|SQL Server, Oracle, Teradata 및 Mongo DB에서 외부 데이터 원본 만들기 |X|X |
|호환 가능한 타사 ODBC 드라이버를 사용하여 외부 데이터 원본 만들기 | | X|
|PolyBase 스케일 아웃 그룹 | X | |
|데이터 풀 인스턴스 | X| |
|스토리지 풀 인스턴스| X| |

>[!NOTE]
>
>ODBC 제네릭 커넥터를 사용하는 연결에 대한 자세한 내용은 [ODBC 제네릭 형식을 구성하는 방법 가이드](polybase-configure-odbc-generic.md)를 참조하세요.

## <a name="whats-new-with-polybase-in-sql-server-2019"></a>SQL Server 2019의 PolyBase에 포함된 새로운 기능은 무엇인가요? 

이제 SQL Server 2019의 PolyBase는 다양한 데이터 원본에서 데이터를 읽을 수 있습니다. 이러한 외부 데이터 원본의 데이터는 SQL Server의 외부 테이블인 저장소일 수 있습니다. PolyBase는 ODBC 제네릭 형식을 제외한 이러한 외부 데이터 원본에 대한 푸시다운 계산을 지원합니다. 

### <a name="compatible-data-sources"></a>호환 가능한 데이터 원본

- SQL Server
- Oracle
- Teradata
- MongoDB
- **호환 가능한** ODBC 제네릭 형식

  > [!NOTE]
  >
  >PolyBase는 타사 ODBC 드라이버를 사용하여 외부 데이터 원본에 연결할 수 있습니다. 이러한 드라이버는 PolyBase와 함께 제공되지 않고 의도한 대로 작동될 수 있습니다. 자세한 내용은 PolyBase ODBC 제네릭 구성에 대한 [가이드](polybase-configure-odbc-generic.md)를 참조하세요.  

## <a name="polybase-vs-linked-servers"></a>PolyBase 및 연결된 서버

|PolyBase | 연결된 서버|
|--------------------------|--------------------------|  
|데이터베이스 범위 지정 개체|인스턴스 범위 지정 개체| 
|ODBC 드라이버 사용|OLEDB 공급 기업 사용| 
| 읽기 전용 작업만 지원합니다. 나중에 확장됨| 읽기 전용 작업만 지원합니다. 나중에 확장됨| 
|쿼리는 스케일 아웃되고 푸시 다운이 지원될 수 있음|쿼리는 단일 스레드이고 푸시 다운이 지원됨|
|Always On 가용성 그룹에 필요한 별도 구성 없음|Always On 가용성 그룹의 각 인스턴스에 필요한 별도 구성|
|기본 인증 전용입니다. SQL Server 2019의 향상된 기능|기본 및 통합 인증|