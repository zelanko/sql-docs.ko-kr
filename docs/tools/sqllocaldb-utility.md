---
title: SqlLocalDB 유틸리티 | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.component: sqllocaldb
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SqlLocalDB utility [SQL Server]
- local database runtime utility
- LocalDB, SqlLocalDB Utility
ms.assetid: d785cdb7-1ea0-4871-bde9-1ae7881190f5
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4c7fb8ffb21b797df1f87486635a92752ea4cdd0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33076610"
---
# <a name="sqllocaldb-utility"></a>SqlLocalDB 유틸리티
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SqlLocalDB** 유틸리티를 사용하여 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssExpCurrent](../includes/ssexpcurrent-md.md)]**LocalDB**의 인스턴스를 만들 수 있습니다. **SqlLocalDB** 유틸리티(SqlLocalDB.exe)는 사용자와 개발자가 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**의 인스턴스를 만들고 관리하는 데 사용할 수 있는 간단한 명령줄 도구입니다. **LocalDB**를 사용하는 방법에 대한 자세한 내용은 [SQL Server 2016 Express LocalDB](../database-engine/configure-windows/sql-server-2016-express-localdb.md)를 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```  
SqlLocalDB.exe   
{  
      [ create   | c ] \<instance-name>  \<instance-version> [-s ]  
    | [ delete   | d ] \<instance-name>  
    | [ start    | s ] \<instance-name>  
    | [ stop     | p ] \<instance-name>  [ -i ] [ -k ]  
    | [ share    | h ] [" <user_SID> " | " <user_account> " ] " \<private-name> " " \<shared-name> "  
    | [ unshare  | u ] " \<shared-name> "  
    | [ info     | i ] \<instance-name>  
    | [ versions | v ]  
    | [ trace    | t ] [ on | off ]  
    | [ help     | -? ]  
}  
```  
  
## <a name="arguments"></a>인수  
 [ **create** | **c** ] *\<instance-name>* *\<instance-version>* [**-s** ]  
 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**의 새 인스턴스를 만듭니다. **SqlLocalDB**는 *\<instance-version>* 인수에 지정된 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 바이너리 버전을 사용합니다. 버전 번호는 하나 이상의 숫자를 포함하는 숫자 형식으로 지정됩니다. 부 버전 번호(서비스 팩)는 선택 사항입니다. 예를 들어 버전 번호 11.0 또는 11.0.1186은 모두 허용됩니다. 지정된 버전을 컴퓨터에 설치해야 합니다. 지정하지 않으면 버전 번호는 기본적으로 **SqlLocalDB** 유틸리티 버전으로 지정됩니다. **–s** 를 추가하여 **LocalDB**의 새 인스턴스를 시작합니다.  
  
 [ **share** | **h** ]  
 지정한 공유 이름을 사용하여 지정한 개인 **LocalDB** 인스턴스를 공유합니다. 사용자 SID 또는 계정 이름을 생략하면 기본값으로 현재 사용자가 사용됩니다.  
  
 [ **unshared** | **u** ]  
 **LocalDB**의 지정된 공유 인스턴스의 공유를 중지합니다.  
  
 [ **delete** | **d** ] *\<instance-name>*  
 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**의 지정된 인스턴스를 삭제합니다.  
  
 [ **start** | **s** ] "*\<instance-name>*"  
 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**의 지정된 인스턴스를 시작합니다. 성공하면 문이 **LocalDB**의 명명된 파이프 주소를 반환합니다.  
  
 [ **stop** | **p** ] *\<instance-name>* [**-i** ] [**-k** ]  
 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**의 지정된 인스턴스를 중지합니다. **–i** 를 **NOWAIT** 옵션과 함께 추가하여 인스턴스 종료를 요청합니다. **–k** 를 추가하면 인스턴스 프로세스에 연결하지 않고 해당 프로세스를 중지합니다.  
  
 [ **info** | **i** ] [ *\<instance-name>* ]  
 현재 사용자가 소유한 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** 의 모든 인스턴스를 나열합니다.  
  
 *\<instance-name>* 은 지정된 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** 인스턴스의 이름, 버전, 상태(실행 중 또는 중지됨), 마지막 시작 시간 및 **LocalDB**의 로컬 파이프 이름을 반환합니다.  
  
 [ **trace** | **t** ] **on** | **off**  
 **trace on**을 사용하여 현재 사용자에 대한 **SqlLocalDB** API 호출을 추적할 수 있습니다. **trace off** 를 사용하면 추적이 사용되지 않습니다.  
  
 **-?**  
 각 **SqlLocalDB** 옵션에 대한 간략한 설명을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 *instance name* 인수는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 식별자에 대한 규칙을 따르거나 큰따옴표로 묶어야 합니다.  
  
 인수 없이 SqlLocalDB를 실행하면 도움말 텍스트가 반환됩니다.  
  
 시작 이외의 작업은 현재 로그인한 사용자에 속하는 인스턴스에 대해서만 수행할 수 있습니다. SQLLOCALDB 인스턴스는 공유하는 경우 인스턴스 소유자만 시작하고 중지할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-an-instance-of-localdb"></a>1. LocalDB의 인스턴스 만들기  
 다음 예에서는 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**바이너리를 사용하여** 라는 `DEPARTMENT` LocalDB [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 의 인스턴스를 만든 다음 인스턴스를 시작합니다.  
  
```  
SqlLocalDB.exe create "DEPARTMENT" 12.0 -s  
```  
  
### <a name="b-working-with-a-shared-instance-of-localdb"></a>2. LocalDB의 공유 인스턴스 작업  
 관리자 권한을 사용하여 명령 프롬프트를 엽니다.  
  
```  
SqlLocalDB.exe create "DeptLocalDB"  
SqlLocalDB.exe share "DeptLocalDB" "DeptSharedLocalDB"  
SqlLocalDB.exe start "DeptLocalDB"  
SqlLocalDB.exe info "DeptLocalDB"  
REM The previous statement outputs the Instance pipe name for the next step  
sqlcmd –S np:\\.\pipe\LOCALDB#<use your pipe name>\tsql\query  
CREATE LOGIN NewLogin WITH PASSWORD = 'Passw0rd!!@52';   
GO  
CREATE USER NewLogin;  
GO  
EXIT  
```  
  
 다음 코드를 실행해서 **로그인을 사용하여** LocalDB `NewLogin` 의 공유 인스턴스에 연결합니다.  
  
```  
sqlcmd –S (localdb)\.\DeptSharedLocalDB -U NewLogin -P Passw0rd!!@52  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2016 Express LocalDB](../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
[명령줄 관리 도구: SqlLocalDB.exe](../relational-databases/express-localdb-instance-apis/command-line-management-tool-sqllocaldb-exe.md)  
  
