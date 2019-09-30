---
title: Oracle 원본 데이터베이스에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraDb
ms.assetid: 220cf555-0db2-443c-8f87-8e413f3ca731
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d49ffcf03fab810eefd190ffea91aa3e5ff38cfe
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298846"
---
# <a name="connect-to-an-oracle-source-database"></a>Oracle 원본 데이터베이스에 연결

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Oracle 원본 페이지를 사용하여 Oracle 원본 데이터베이스에 연결하는 데 필요한 정보를 제공할 수 있습니다. CDC 인스턴스는 연결된 Oracle 데이터베이스의 다시 실행 로그를 읽습니다.  
  
 **Oracle 연결 문자열**  
 사용 중인 Oracle 데이터베이스가 있는 컴퓨터에 대한 Oracle 연결 문자열을 입력합니다. 연결 문자열은 다음 중 한 가지 방법으로 작성됩니다.  
  
 `host[:port][/service name]`  
  
 연결 문자열에서 Oracle Net 연결 설명자를 지정할 수도 있습니다(예: `(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp) (HOST=erp.contoso.com) (PORT=1521)) (CONNECT_DATA=(SERVICE_NAME=orcl)))`  
  
 디렉터리 서버 또는 tnsnames를 사용하는 경우 연결 문자열이 연결의 이름일 수 있습니다.  
  
 **Oracle 로그 마이닝 인증**  
 로그 마이닝에 대한 권한이 있는 Oracle 데이터베이스 사용자의 자격 증명을 입력하려면 다음 중 하나를 선택합니다.  
  
-   **Windows 인증**: 현재 Windows 도메인 자격 증명을 사용하려면 선택합니다. Windows 인증을 사용하도록 Oracle 데이터베이스를 구성한 경우에만 이 옵션을 사용할 수 있습니다.  
  
-   **Oracle 인증**: 이 옵션을 선택하는 경우 연결 중인 Oracle 데이터베이스의 사용자에 대한 **사용자 이름**과 **암호**를 입력해야 합니다.  
  
> [!NOTE]
>  사용자가 로그 마이닝 사용자가 되려면 Oracle 데이터베이스에 다음 권한이 부여되어야 합니다.  
> 
>  -   \<any-captured-table>에 대한 SELECT 권한  
> -   SELECT ANY TRANSACTION  
> -   DBMS LOGMNR에 대한 EXECUTE 권한  
> -   V$LOGMNR CONTENTS에 대한 SELECT 권한  
> -   V$ARCHIVED LOG에 대한 SELECT 권한  
> -   V$LOG에 대한 SELECT 권한  
> -   V$LOGFILE에 대한 SELECT 권한  
> -   V$DATABASE에 대한 SELECT 권한  
> -   V$THREAD에 대한 SELECT 권한  
> -   ALL INDEXES에 대한 SELECT 권한  
> -   ALL OBJECTS에 대한 SELECT 권한  
> -   DBA OBJECTS에 대한 SELECT 권한  
> -   ALL TABLES에 대한 SELECT 권한  
> 
>  이러한 권한을 V$xxx에 부여할 수 없는 경우 V_S$xxx에 부여합니다.  
  
 **연결 테스트**  
 **연결 테스트** 를 클릭하여 Oracle 데이터베이스가 있는 원격 컴퓨터와의 연결되었는지 여부를 확인할 수 있습니다. 연결에 성공했는지 여부를 알려주는 대화 상자가 열립니다.  
  
> [!IMPORTANT]  
>  CDC Designer를 관리자 권한으로 실행하지 않을 경우 알려진 문제로 인해 Oracle 원본 데이터베이스에 연결하지 못할 수 있습니다. 연결이 실패하는 경우 CDC Designer를 닫은 후 **관리자 권한으로 실행** 옵션을 사용하여 다시 시작합니다.  
  
 이 페이지에서 정보 입력을 마친 후 **다음** 을 클릭하여 [Select Oracle Tables and Columns](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)을 수행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 변경 데이터베이스 인스턴스를 만드는 방법](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [인스턴스 속성 편집](../../integration-services/change-data-capture/edit-instance-properties.md)  
  
  
