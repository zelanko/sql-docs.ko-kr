---
title: Active Directory 모드에서 빅 데이터 클러스터 액세스 관리
description: 빅 데이터 클러스터 액세스 관리
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/04/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ef2df0bec343d73de90a43e411da92530c3c50c8
ms.sourcegitcommit: 6ab28d954f3a63168463321a8bc6ecced099b247
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/05/2020
ms.locfileid: "87790273"
---
# <a name="manage-big-data-cluster-access-in-active-directory-mode"></a>Active Directory 모드에서 빅 데이터 클러스터 액세스 관리

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 배포 시 *clusterUsers* 구성 설정을 통해 제공된 그룹 외에 *bdcUser* 역할의 새 Active Directory 그룹을 추가하는 방법을 설명합니다.

>[!IMPORTANT]
>이 절차를 사용하여 *bdcAdmin* 역할의 새 Active Directory 그룹을 추가하지 마세요. HDFS 및 Spark와 같은 Hadoop 구성 요소는 단일 Active Directory 그룹을 슈퍼 사용자 그룹(BDC의 *bdcAdmin* 역할에 해당)으로 허용합니다. 배포 후 추가 Active Directory 그룹에 빅 데이터 클러스터에 대한 *bdcAdmin* 권한을 부여하려면 배포하는 동안 이미 지정한 그룹에 사용자 및 그룹을 더 추가해야 합니다. 동일한 절차에 따라 *bdcUsers* 역할이 있는 그룹 구성원 자격을 업데이트할 수 있습니다.

## <a name="two-overarching-roles-in-the-big-data-cluster"></a>빅 데이터 클러스터의 두 가지 주요 역할

빅 데이터 클러스터 내에서 권한 부여를 위한 두 가지 주요 역할의 일부로 배포 프로필의 보안 섹션에서 Active Directory 그룹을 제공할 수 있습니다.

* `clusterAdmins`: 이 매개 변수는 하나의 Active Directory 그룹을 사용합니다. 이 그룹의 구성원에는 *bdcAdmin* 역할이 있으므로 전체 클러스터에 대한 관리자 권한을 얻게 됩니다. SQL Server의 *sysadmin* 권한, HDFS(Hadoop 분산 파일 시스템) 및 Spark의 *superuser* 권한 및 컨트롤러의 *관리자* 권한이 있습니다.

* `clusterUsers`: 이러한 Active Directory 그룹은 BDC의 *bdcUsers* 역할에 매핑됩니다. 이들은 클러스터에서 관리자 권한이 없는 일반 사용자입니다. SQL Server 마스터 인스턴스에 로그인할 수 있는 권한이 있지만 기본적으로 개체 또는 데이터에 대한 사용 권한은 없습니다. 이들은 슈퍼 사용자 권한이 없는 HDFS 및 Spark 일반 사용자입니다. 컨트롤러 엔드포인트에 연결하는 경우 이러한 사용자는 엔드포인트를 쿼리할 수 있습니다(azdata bdc 엔드포인트 목록을 사용).

Active Directory 내에서 그룹 멤버 자격을 변경하지 않고 추가 Active Directory 그룹에 *bdcUser* 권한을 부여하려면 다음 섹션의 절차를 완료합니다.

## <a name="grant-bdcuser-permissions-to-additional-active-directory-groups"></a>추가 Active Directory 그룹에 *bdcUser* 권한 부여

### <a name="create-a-login-for-the-active-directory-user-or-group-in-the-sql-server-master-instance"></a>SQL Server 마스터 인스턴스에서 Active Directory 사용자 또는 그룹에 대한 로그인 만들기

1. 즐겨 사용하는 SQL 클라이언트를 사용하여 마스터 SQL 엔드포인트에 연결합니다. 관리자 로그인을 사용합니다(예: 배포 중에 제공된 `AZDATA_USERNAME`). 또는 보안 구성에서 `clusterAdmins`로 제공되는 Active Directory 그룹에 속하는 모든 Active Directory 계정일 수 있습니다.

1. Active Directory 사용자 또는 그룹에 대한 로그인을 만들려면 다음 TSQL 명령을 실행합니다.

   ```sql
   CREATE LOGIN [<domain>\<principal>] FROM WINDOWS;
   ```

   SQL Server 인스턴스에서 원하는 사용 권한을 부여합니다.

   ```sql
   ALTER SERVER ROLE <server role> ADD MEMBER [<domain>\<principal>];
   GO
   ```

전체 서버 역할 목록은 [여기](../relational-databases/security/authentication-access/server-level-roles.md)에서 해당 SQL Server 보안 항목을 참조하세요.

### <a name="add-the-active-directory-user-or-group-to-the-roles-table-in-the-controller-database"></a>컨트롤러 데이터베이스의 역할 테이블에 Active Directory 사용자 또는 그룹 추가

1. 다음 명령을 실행하여 컨트롤러 SQL Server 자격 증명을 가져옵니다.

   a. 이 명령을 Kubernetes 관리자 권한으로 실행합니다.

   ```bash
   kubectl get secret controller-sa-secret -n <cluster name> -o yaml | grep password
   ```

   b. 암호를 Base64 디코드합니다.

   ```bash
   echo <password from kubectl command>  | base64 --decode && echo
   ```

1. 별도의 명령 창에서 컨트롤러 데이터베이스 서버 포트를 공개합니다.

   ```bash
   kubectl port-forward controldb-0 1433:1433 --address 0.0.0.0 -n <cluster name>
   ```

1. 위의 연결을 사용하여 *roles* 및 *active_directory_principals* 테이블에 새 행을 삽입합니다. *REALM* 값을 대문자로 입력합니다.

   ```sql
   USE controller;
   GO

   INSERT INTO [controller].[auth].[roles] VALUES (N'<user or group name>@<REALM>', 'bdcUser')
   GO

   INSERT INTO [controller].[auth].[active_directory_principals] VALUES (N'<user or group name>@<REALM>', N'<SID>')
   GO
   ```

   추가되는 사용자 또는 그룹의 SID를 찾으려면 [Get-ADUser](/powershell/module/addsadministration/get-aduser/) 또는 [Get-ADGroup](/powershell/module/addsadministration/get-adgroup/) PowerShell 명령을 사용하면 됩니다.

2. 컨트롤러 엔드포인트 로그인 또는 SQL Server 마스터 인스턴스에 대한 인증을 사용하여 추가한 그룹의 구성원에게 예상된 *bdcUser* 권한이 있는지 확인합니다. 예를 들면 다음과 같습니다.

   ```bash
   azdata login
   azdata bdc endpoints list
   ```

## <a name="next-steps"></a>다음 단계

- [SQL Server 2019 빅 데이터 클러스터의 보안 개념](concept-security.md)
