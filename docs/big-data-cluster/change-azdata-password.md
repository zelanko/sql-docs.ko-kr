---
title: AZDATA_PASSWORD 업데이트
description: 수동으로 `AZDATA_PASSWORD` 업데이트
author: NelGson
ms.author: negust
ms.reviewer: mikeray
ms.date: 12/19/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1cc2a7778100be5c919c86a4c949d5aeb784d8e5
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76265995"
---
# <a name="manually-update-azdata_password"></a>수동으로 `AZDATA_PASSWORD` 업데이트

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

클러스터가 Active Directory 통합으로 작동하는지 여부에 관계없이 배포 중에 `AZDATA_PASSWORD`가 설정됩니다. 이는 클러스터 컨트롤러 및 마스터 인스턴스에 대한 기본 인증을 제공합니다. 이 문서에서는 `AZDATA_PASSWORD`를 수동으로 업데이트하는 방법을 설명합니다.

## <a name="change-azdata_password-for-controller"></a>컨트롤러에 대한 `AZDATA_PASSWORD` 변경

클러스터가 Active Directory 모드가 아닌 모드로 작동하는 경우 다음을 수행하여 Apache Knox 게이트웨이 암호를 업데이트합니다.

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
 
1. 방금 얻은 시스템 관리자 암호를 사용하여 SQL 클라이언트 도구에서 컨트롤러 데이터베이스 서버에 연결합니다.

1. `AZDATA_USERNAME`에 대한 새 복합 암호를 생성하여 기존 `AZDATA_PASSWORD`를 바꿉니다.

   예제를 간소화하기 위해, 생성된 암호가 "newPassword"이므로 다음 단계에서는 "newPassword"를 사용합니다. 

1. 사용자 테이블에서 `hexsalt`를 가져옵니다.

   ```sql
   SELECT hexsalt FROM [auth].[users] WHERE username = '<username>'
   ```

   `hexsalt`는 임의의 16진수 문자열을 반환합니다(예: `64FC59DF31244FFEE02F457BC0750226`).

1. `hexsalt`를 사용하여 새 복합 암호를 암호화합니다.

   사용자의 편의를 위해 암호를 암호화하는 미리 작성된 도구 `pbkdf2`가 제공됩니다. 플랫폼에 적합한 [`pbkdf2`](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/security/password-hashing/pbkdf2/prebuilt-binaries)용 .NET Core 앱을 다운로드합니다.

   앱은 자체 포함식이며 .NET 런타임과 같은 필수 구성 요소가 필요하지 않습니다. 암호를 암호화하려면 다음을 실행합니다.

   ```bash
   pbkdf2 <password> <hexsalt>
   J2y4E4dhlgwHOaRr3HKiiVAKBfjuGDyYmzn88VXmrzM=
   ```

1. 사용자 테이블에서 암호를 업데이트합니다.

   ```SQL
   UPDATE [auth].[users] SET password = 'J2y4E4dhlgwHOaRr3HKiiVAKBfjuGDyYmzn88VXmrzM=' WHERE username = '<username>'
   ```

## <a name="change-azdata_password-in-the-sql-server-master-instance"></a>SQL Server 마스터 인스턴스에서 `AZDATA_PASSWORD` 변경

1. 모든 관리자 사용자를 사용하여 마스터 SQL 엔드포인트에 연결합니다.

1. 배포 시 매개 변수 `AZDATA_USERNAME`에서 정의한 로그인 자격 증명에 대한 암호를 변경하려면 다음 TSQL 명령을 실행합니다.

   ```sql
   ALTER LOGIN <AZDATA_USERNAME> WITH PASSWORD = 'newPassword'
   ```
