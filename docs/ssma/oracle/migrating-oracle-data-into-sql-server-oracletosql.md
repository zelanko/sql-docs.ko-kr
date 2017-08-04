---
title: "Oracle 데이터를 SQL Server (OracleToSQL)로 마이그레이션 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle Data Migration, Client-Side Migration
- Oracle Data Migration,Server-Side Migration
ms.assetid: e23c5268-41ed-4e55-9fe7-a11376202a13
caps.latest.revision: 13
author: sabotta
ms.author: carlasab
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 10c7bfea3316146924544a7c76d3bc727006b694
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="migrating-oracle-data-into-sql-server-oracletosql"></a>Oracle 데이터를 SQL Server (OracleToSQL)로 마이그레이션
으로 변환 된 개체를 성공적으로 동기화 한 후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Oracle에서 데이터를 마이그레이션할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
> [!IMPORTANT]  
> 서버 쪽 데이터 마이그레이션 엔진으로 사용 하 고 엔진을 사용 하는 경우, 데이터를 마이그레이션할 수 있습니다 설치 해야 합니다는 SSMA Oracle 확장 팩 및 SSMA를 실행 하는 컴퓨터에 Oracle 공급자에 대 한 합니다. 도 SQL Server 에이전트 서비스를 실행 해야 합니다. 확장 팩을 설치 하는 방법에 대 한 자세한 내용은 참조 [서버 구성 요소 (OracleToSQL) 설치](http://msdn.microsoft.com/en-us/33070e5f-4e39-4b70-ae81-b8af6e4983c5)  
  
## <a name="setting-migration-options"></a>마이그레이션 옵션 설정  
마이그레이션을 수행 하기 전에 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에 프로젝트 마이그레이션 옵션을 검토 하는 **프로젝트 설정** 대화 상자.  
  
-   이 대화 상자를 사용 하 여 마이그레이션 일괄 처리 크기, 테이블 잠금, 제약 조건 검사, null 값 처리 및 id 값 처리 등의 옵션을 설정할 수 있습니다. 프로젝트 마이그레이션 설정에 대 한 자세한 내용은 참조 [프로젝트 설정 (마이그레이션) (OracleToSQL)](http://msdn.microsoft.com/en-us/fcd6b988-633b-4b2b-9f36-6368b5e86b60)합니다.  
  
-   **마이그레이션 엔진** 에 **프로젝트 설정** 대화 상자의 두 가지 유형의 데이터 마이그레이션 엔진을 사용 하 여 마이그레이션 프로세스를 수행할 수 있습니다.  
  
    1.  클라이언트 쪽 데이터 마이그레이션 엔진  
  
    2.  서버 쪽 데이터 마이그레이션 엔진  
  
**클라이언트 쪽 데이터 마이그레이션:**  
  
-   클라이언트 쪽에서 데이터 마이그레이션을 시작 하려면 선택은 **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션에 **프로젝트 설정** 대화 상자.  
  
-   **프로젝트 설정**, **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션을 설정 합니다.  
  
    > [!NOTE]  
    > **클라이언트 쪽 데이터 마이그레이션 엔진** SSMA 응용 프로그램 내에 상주 하며 따라서 확장 팩의 가용성에 종속 되지 않습니다.  
  
**서버 쪽 데이터 마이그레이션:**  
  
-   서버 쪽 데이터 마이그레이션 중에 엔진은 대상 데이터베이스에 상주합니다. 확장 팩을 통해 설치 됩니다. 확장 팩을 설치 하는 방법에 대 한 자세한 내용은 참조 하세요. [SQL Server에서 서버 구성 요소 설치](http://msdn.microsoft.com/en-us/33070e5f-4e39-4b70-ae81-b8af6e4983c5)  
  
-   서버 쪽에서 마이그레이션을 시작 하려면 선택은 **서버 쪽 데이터 마이그레이션 엔진** 옵션에 **프로젝트 설정** 대화 상자.  
  
## <a name="migrating-data-to-sql-server"></a>SQL Server로 데이터 마이그레이션  
마이그레이션 데이터는 Oracle 테이블에서 행의 데이터를 이동 하는 대량 로드 작업 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 트랜잭션에서 테이블입니다. 에 로드 된 행의 수 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 각 트랜잭션에서 프로젝트 설정에서 구성 됩니다.  
  
마이그레이션 메시지를 보려면 출력 창이 표시 되는지 확인 합니다. , 그렇지 않으면는 **보기** 메뉴 선택 **출력**합니다.  
  
**데이터를 마이그레이션**  
  
1.  다음을 확인합니다.  
  
    -   Oracle 공급자 SSMA를 실행 하는 컴퓨터에 설치 됩니다.  
  
    -   변환된 된 개체와 동기화 했다면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터베이스입니다.  
  
2.  Oracle 메타 데이터 탐색기에서 마이그레이션할 데이터가 포함 된 개체를 선택 합니다.  
  
    -   모든 스키마에 대 한 데이터를 마이그레이션하려면 확인란을 옆에 선택 **스키마**합니다.  
  
    -   데이터를 마이그레이션하거나 생략 개별 테이블을 먼저 스키마를 확장 하 고 **테이블**, 다음을 선택 하거나 테이블 옆 확인란의 선택을 취소 합니다.  
  
3.  데이터를 마이그레이션하려면 두 가지 경우 발생 합니다.  
  
    **클라이언트 쪽 데이터 마이그레이션:**  
  
    -   수행 하기 위한 **클라이언트 쪽 데이터 마이그레이션**을 선택는 **클라이언트 쪽 데이터 마이그레이션 엔진** 옵션에 **프로젝트 설정** 대화 상자.  
  
    **서버 쪽 데이터 마이그레이션:**  
  
    -   를 서버 쪽에서 데이터 마이그레이션을 수행 하기 전에 다음을 확인 합니다.  
  
        1.  Oracle 확장 팩 용 SSMA의 인스턴스에 설치 되어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
        2.  SQL Server의 인스턴스에서 SQL Server 에이전트 서비스 실행 중입니다.  
  
    -   수행 하기 위한 **서버 쪽 데이터 마이그레이션**을 선택는 **서버 쪽 데이터 마이그레이션 엔진** 옵션에 **프로젝트 설정** 대화 상자.  
  
4.  마우스 오른쪽 단추로 클릭 **스키마** Oracle 메타 데이터 탐색기에서를 클릭 한 다음 **데이터 마이그레이션**합니다. 개별 개체 또는 개체의 범주에 대 한 데이터를 마이그레이션할 수도 있습니다: 개체 또는 해당 부모 폴더를 마우스 오른쪽 단추로 클릭 선택 된 **데이터 마이그레이션** 옵션입니다.  
  
    > [!NOTE]  
    > Oracle 확장 팩 용 SSMA의 인스턴스에 설치 되지 않습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]를 쓰고 **서버 쪽 데이터 마이그레이션 엔진** 을 선택한 경우 대상 데이터베이스에 데이터를 마이그레이션하는 동안 다음 오류가 발생: ' SSMA 데이터 마이그레이션 구성 요소를 찾을 수 없습니다 SQL Server, 서버 쪽 데이터 마이그레이션 지원 되지 것입니다. 확장 팩 올바르게 설치 되어 있는지를 확인 하십시오. '. 클릭 **취소** 데이터 마이그레이션을 종료 하 합니다.  
  
5.  에 **Connect to Oracle** 대화 상자에서 연결 자격 증명을 입력 한 다음 클릭 **연결**합니다. Oracle에 연결 하는 방법에 대 한 자세한 내용은 참조 하세요. [Oracle에 연결 &#40; OracleToSQL &#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md)  
  
    대상 데이터베이스에 연결 하기 위한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]에 연결 자격 증명을 입력의 **SQL Server에 연결** 대화 상자와 클릭 **연결**합니다. 연결에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], 참조 [SQL Server에 연결](http://msdn.microsoft.com/en-us/bb8c4bde-cfc2-4636-92ae-5dd24abe9536)  
  
    메시지에 표시 됩니다는 **출력** 창. 마이그레이션이 완료 되는 **데이터 마이그레이션 보고서** 나타납니다. 모든 데이터 마이그레이션하지 않은 경우 오류를 포함 하는 행을 클릭 한 다음 클릭 **세부 정보**합니다. 보고서와 함께 완료 했으면 클릭 **닫기**합니다. 데이터 마이그레이션 보고서에 대 한 자세한 내용은 참조 하십시오. [(SSMA 공통) 데이터 마이그레이션 보고서](http://msdn.microsoft.com/en-us/bbfb9d88-5a98-4980-8d19-c5d78bd0d241)  
  
> [!NOTE]  
> SQL Express edition으로 대상 데이터베이스를 사용 하면 클라이언트 쪽 데이터 마이그레이션에만 사용할 수 및 서버 쪽 데이터 마이그레이션이 지원 되지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server &#40; OracleToSQL &#41; Oracle 데이터베이스 마이그레이션](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  

