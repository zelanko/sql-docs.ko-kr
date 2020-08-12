---
title: Active Directory 모드에서 빅 데이터 클러스터 액세스 관리
description: 빅 데이터 클러스터 액세스 관리
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 12/06/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 94719ef65023b1afd4edcf7770887323d0267127
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730620"
---
# <a name="manage-big-data-cluster-access-in-active-directory-mode"></a>Active Directory 모드에서 빅 데이터 클러스터 액세스 관리

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 clusterAdmins 및 clusterUsers를 배포하는 동안 제공되는 Active Directory 그룹을 업데이트하는 방법에 대해 설명합니다.

## <a name="two-overarching-roles-in-the-big-data-cluster"></a>빅 데이터 클러스터의 두 가지 주요 역할

빅 데이터 클러스터 내에서 권한 부여를 위한 두 가지 주요 역할의 일부로 배포 프로필의 보안 섹션에서 Active Directory 그룹을 제공할 수 있습니다.

* `clusterAdmins`: 이 매개 변수는 하나의 Active Directory 그룹을 사용합니다. 이 그룹의 멤버는 전체 클러스터에 대한 관리자 권한을 얻습니다. SQL Server의 *sysadmin* 권한, HDFS(Hadoop 분산 파일 시스템) 및 Spark의 *superuser* 권한 및 컨트롤러의 *관리자* 권한이 있습니다.

* `clusterUsers`: 이러한 Active Directory 그룹은 클러스터에서 관리자 권한이 없는 일반 사용자입니다. SQL Server 마스터 인스턴스에 로그인할 수 있는 권한이 있지만 기본적으로 개체 또는 데이터에 대한 사용 권한은 없습니다.

배포 후에 빅 데이터 클러스터에 추가 Active Directory 그룹 권한을 부여하는 한 가지 방법은 배포하는 동안 이미 지정한 그룹에 사용자 및 그룹을 더 추가하는 것입니다. 

그러나 관리자가 Active Directory 내에서 그룹 멤버 자격을 변경하는 것이 항상 가능한 것은 아닙니다. Active Directory 내에서 그룹 멤버 자격을 변경하지 않고 추가 Active Directory 그룹 권한을 부여하려면 다음 섹션의 절차를 완료합니다.

## <a name="grant-administrator-permissions-to-additional-active-directory-groups"></a>추가 Active Directory 그룹에 관리자 권한 부여

>[!IMPORTANT]
>이 절차는 추가 Active Directory 그룹 관리자에게 빅 데이터 클러스터의 HDFS 및 Spark와 같은 Hadoop 구성 요소에 대한 액세스 권한을 부여하지 않습니다. 이러한 구성 요소는 한 개의 Active Directory 그룹을 슈퍼 사용자 그룹으로 허용합니다. 이 제한 사항은 배포 중에 `clusterAdmins`에 지정된 그룹이 이 단계를 수행한 후에도 슈퍼 사용자 그룹으로 유지됨을 의미합니다.

이 섹션의 절차에 따라 컨트롤러와 SQL Server 마스터 인스턴스 모두에 대한 관리자 액세스 권한을 부여할 수 있습니다.

### <a name="create-a-login-for-the-active-directory-user-or-group-in-the-sql-server-master-instance"></a>SQL Server 마스터 인스턴스에서 Active Directory 사용자 또는 그룹에 대한 로그인 만들기 

1. 즐겨 사용하는 SQL 클라이언트를 사용하여 마스터 SQL 엔드포인트에 연결합니다. 관리자 로그인을 사용합니다(예: 배포 중에 제공된 `AZDATA_USERNAME`). 또는 보안 구성에서 `clusterAdmins`로 제공되는 Active Directory 그룹에 속하는 모든 Active Directory 계정일 수 있습니다.

1. Active Directory 사용자 또는 그룹에 대한 로그인을 만들려면 다음 TSQL 명령을 실행합니다.

   ```sql
   CREATE LOGIN [<domain>\<principal>] FROM WINDOWS;
   ```

   SQL Server 인스턴스에서 관리자 권한을 부여하는 경우 다음 권한도 부여합니다.

   ```sql
   ALTER SERVER ROLE sysadmin ADD MEMBER [<domain>\<principal>];
   GO
   ```

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

1. 위의 연결을 사용하여 역할 테이블에 행을 삽입합니다. *REALM* 값을 대문자로 입력합니다.

   관리자 권한을 부여하는 경우 *\<role name>* 에 *bdcAdmin* 역할을 사용합니다. 비관리자 사용자의 경우 *bdcUser* 역할을 사용합니다.

   ```sql
   USE controller;
   GO

   INSERT INTO [controller].[auth].[roles] VALUES (N'<user or group name>@<REALM>', N'<role name>')
   GO
   ```

1. 컨트롤러 엔드포인트에 로그인하고 다음 명령을 실행하여 추가한 그룹의 멤버가 빅 데이터 클러스터 관리자 권한을 가지고 있는지 확인합니다.

   ```bash
   azdata bdc config show
   ```

1. 비관리자 사용자의 경우 `azdata login`을 통해 SQL 마스터 인스턴스나 컨트롤러에 인증하여 액세스를 확인할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [SQL Server 2019 빅 데이터 클러스터의 보안 개념](concept-security.md)
