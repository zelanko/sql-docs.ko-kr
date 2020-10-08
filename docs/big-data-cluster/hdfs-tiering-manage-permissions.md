---
title: SQL Server 빅 데이터 클러스터에 대한 HDFS 계층화 권한
titleSuffix: Manage HDFS tiering permissions for SQL Server Big Data Clusters
description: SQL Server 빅 데이터 클러스터에서 다른 Linux 기반 시스템의 권한을 비롯해 HDFS 계층화에 대한 보안을 관리합니다.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 126bb1ae7daddbaeb4d0ab72440051807f71cd5c
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725834"
---
# <a name="manage-hdfs-permissions-for-big-data-clusters-2019"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 HDFS 권한 관리

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

파일 시스템으로서의 HDFS는 파일 권한을 위해 POSIX를 사용하는 Linux 기반 파일 시스템과 비슷합니다. HDFS는 기존의 POSIX 권한 모델 외에도 POSIX ACL(액세스 제어 목록)을 지원합니다. 자세한 내용은 [ACL에 관한 Apache Hadoop 문서](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_.28Access_Control_Lists.29)를 참조하세요.

이어지는 섹션에서는 `azdata` CLI를 사용하여 HDFS 파일 및 디렉터리 권한을 관리하는 방법을 설명하는 예제를 보여 줍니다.

## <a name="prerequisites"></a>사전 요구 사항

- [빅 데이터 클러스터 배포](deployment-guidance.md)
- [빅 데이터 도구](deploy-big-data-tools.md)
  
## <a name="hdfs-shell"></a>HDFS 셸

`azdata`의 `hdfs` 셸 기능을 사용하면 파일 및 디렉터리에 대한 HDFS 권한을 관리하는 명령을 셸에서 직접 실행할 수 있습니다. 기본 메커니즘은 WebHdfs 호출을 사용하여 명령을 실행합니다.

다음 명령을 실행하면 셸이 열립니다.

```bash
azdata bdc hdfs shell
```

`hdfs` 셸 도움말을 열고 명령을 실행하는 방법을 이해하려면 셸이 활성화된 후에 다음 명령을 실행합니다.

```bash
[hdfs] ?
```

다음 예제에서는 디렉터리를 만들고, 디렉터리를 나열하고, 디렉터리에 대한 권한을 수정하고, 명명된 사용자 `bob`에게 디렉터리 `sales`에 대한 읽기, 쓰기 및 실행 권한을 부여하는 방법을 보여 줍니다.

```bash
[hdfs] mkdir sales
[hdfs] ls
rwxr-xr-x  hdfs bdcadmins        0 Oct 09 18:02 system/
rwxrwxr-x admin bdcadmins        0 Oct 10 16:47 sales/
--xrwxrwxrwx  hdfs bdcadmins        0 Oct 09 18:03 tmp/
rwxrwxrwx  hdfs bdcadmins        0 Oct 09 17:59 user/

[hdfs] acl modify  '/sales/' 'user:bob:rwx'
acl modify: Change completed.
[hdfs] acl status  '/sales/'
{
  `AclStatus`: {
    `entries`: [
      `user:bob:rwx`,
      `group::r-x`
    ],
    `group`: `bdcadmins`,
    `owner`: `admin`,
    `permission`: `775`,
    `stickyBit`: false
  }
}
```

## <a name="create-a-directory-in-hdfs-using-azdata"></a>`azdata`를 사용하여 HDFS에 디렉터리 만들기

경로 `/sales`에 디렉터리 `data`를 만듭니다.

```bash
azdata bdc hdfs mkdir --path '/sales/data'
```

## <a name="change-owner-of-a-directory-or-file"></a>디렉터리 또는 파일의 소유자 변경

HDFS에서 `data` 디렉터리의 소유 사용자를 변경하여 *`alice`* 를 소유 사용자로, *`salesgroup`* 을 소유 그룹으로 만듭니다. 소유자 변경은 소유자만 수행할 수 있습니다.

```bash
azdata bdc hdfs chown --owner alice --group 'salesgroup' --path '/sales/data'
```

## <a name="change-permissions-of-a-file-or-directory-with-chmod"></a>`chmod`를 사용하여 파일 또는 디렉터리의 권한 변경

`chmod`를 사용하여 파일 및 디렉터리에 관한 소유자, 소유 그룹 등의 권한을 변경합니다. 자세한 내용은 [Linux 파일 시스템에서 권한 변경](https://www.lifewire.com/uses-of-command-chmod-2201064)을 참조하세요. HDFS에서도 패턴은 동일합니다. 다음은 그 예입니다.

```bash
azdata bdc hdfs chmod --permission 750 --path /sales/data
```

```bash
azdata bdc hdfs chmod --permission 775 --path /sales/data/file.txt
```

## <a name="set-sticky-bit-on-directories"></a>디렉터리에 고정 비트 설정

의도치 않은 파일 삭제나 재배치가 이루어지지 않도록 디렉터리에 고정 비트를 설정합니다. 고정 비트는 파일의 삭제 또는 이동 권한을 슈퍼 사용자, 디렉터리 소유자 또는 파일 소유자로 제한합니다. 이 설정은 파일에 영향을 주지 않습니다. 다음 예제에서는 권한에 접두사 `1`를 붙여서 디렉터리 `users`에 고정 비트를 설정합니다.

```bash
azdata bdc hdfs chmod --path /sales/users --permission 1750
```

## <a name="setting-acls-on-files-and-directories"></a>파일 및 디렉터리에 ACL 설정

HDFS에서 파일 및 디렉터리에 ACL을 설정하려면 `azdata` 명령을 사용합니다.

디렉터리에 ACL을 설정하고 명명된 사용자 *`tom`* 에게 디렉터리 *`data`* 에 대한 읽기, 쓰기 및 실행 권한을 부여합니다. 

> [!NOTE]
> `set` 명령을 사용할 때는 소유 사용자, 소유 그룹 등에 ACL 사양을 포함한 전체 ACL 사양을 부여해야 합니다.

```bash
azdata bdc hdfs acl set --path '/sales' --aclspec  'user::rw-,user:tom:rwx,group::rw-,other::rw-'
```

## <a name="default-acl-on-directories"></a>디렉터리의 기본 ACL

기본 ACL을 사용하면 하위 디렉터리가 상위 디렉터리의 권한을 상속받을 수 있습니다. 기본 ACL은 디렉터리에만 있을 수 있습니다. 새 파일 또는 하위 디렉터리가 생성되면 상위 디렉터리의 기본 ACL이 자기 자신의 액세스 ACL로 자동 상속됩니다. 새로운 하위 디렉터리가 생성됨에 따라 계속해서 매우 깊은 디렉터리 수준까지 기본 ACL이 상속될 수 있습니다.

다음은 azdata를 사용하여 기본 ACL을 설정하는 예입니다.

```bash
azdata bdc hdfs acl set --path '/sale' --aclspec  'user::rw-,user:tom:rwx,group::rw-,other::rw-,default:group::rw-,default:user::rw-,default:other::rw-'
```

## <a name="next-steps"></a>다음 단계

- [`azdata` 참조](../azdata/reference/reference-azdata.md)

- [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란 무엇인가요?](big-data-cluster-overview.md)