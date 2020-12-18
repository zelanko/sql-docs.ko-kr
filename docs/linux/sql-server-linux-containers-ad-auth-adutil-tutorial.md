---
title: adutil을 사용하여 SQL Server on Linux 기반 컨테이너에서 Active Directory 인증 구성
description: adutil을 사용하여 SQL Server on Linux 컨테이너에서 Active Directory 인증을 구성하는 방법에 대한 단계별 지침
author: amvin87
ms.author: amitkh
ms.reviewer: vanto
ms.date: 12/10/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 318fb046adc25cc2ff485b14974bb756e586162b
ms.sourcegitcommit: 18e2f0706e03d0b2b6324845244fbafaa077a8dd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97103307"
---
# <a name="tutorial-configure-active-directory-authentication-with-sql-server-on-linux--containers"></a>자습서: SQL Server on Linux 컨테이너에서 Active Directory 인증 구성

> [!NOTE]
> **adutil** 은 현재 **퍼블릭 미리 보기** 로 제공됩니다.

이 자습서에서는 통합 인증이라고도 하는 AD(Active Directory) 인증을 지원하도록 SQL Server on Linux 컨테이너를 구성하는 방법을 설명합니다. 개요에 대해서는 [Linux의 SQL Server에 대한 Active Directory 인증](sql-server-linux-active-directory-auth-overview.md)을 참조하세요.

이 자습서는 다음 작업으로 구성됩니다.

> [!div class="checklist"]
> - adutil-preview 설치
> - AD 도메인에 Linux 호스트 조인
> - adutil 도구를 사용하여 SQL Server의 AD 사용자 만들기 및 SPN(ServicePrincipalName) 설정
> - SQL Server 서비스 keytab 파일 만들기
> - SQL Server 컨테이너에서 사용할 mssql.conf 및 krb5.conf 파일 만들기
> - 구성 파일 탑재 및 SQL Server 컨테이너 배포
> - Transact-SQL을 사용하여 AD 기반 SQL Server 로그인 만들기
> - AD 인증을 사용하여 SQL Server에 연결

## <a name="prerequisites"></a>필수 구성 요소

AD 인증을 구성하려면 다음 항목이 필요합니다.

- 네트워크에 AD 도메인 컨트롤러(Windows)가 있음.
- 도메인에 조인된 Linux 호스트 머신에 adutil-preview 도구 설치. adutil-preview 도구를 설치하기 위해 실행 중인 Linux 배포에 따라 아래의 [adutil-preview 설치](#install-adutil-preview) 섹션을 수행합니다.

## <a name="container-deployment-and-preparation"></a>컨테이너 배포 및 준비

컨테이너를 설정하려면 호스트의 컨테이너에서 사용할 포트를 미리 알고 있어야 합니다. 기본 포트인 1433은 컨테이너 호스트에서 다르게 매핑될 수 있습니다. 이 자습서에서는 호스트의 포트 5433이 컨테이너의 포트 1433에 매핑됩니다. 자세한 내용은 [Docker에서 SQL Server 컨테이너 이미지 실행](quickstart-install-connect-docker.md) 빠른 시작을 참조하세요.

SPN(서비스 사용자 이름)을 등록할 때 머신의 호스트 이름 또는 컨테이너의 이름을 사용할 수 있지만 외부에서 컨테이너에 연결할 때 표시하려는 항목에 따라 설정해야 합니다.

SQL Server 컨테이너의 이름에 매핑되는 Linux 호스트 IP 주소에 대해 Active Directory에서 추가된 전달 호스트(A) 항목이 있는지 확인합니다. 이 자습서에서 `myubuntu` 호스트 머신의 IP 주소는 `10.0.0.10`이고 SQL Server 컨테이너 이름은 `sql1`입니다. 다음과 같이 Active Directory에서 전달 호스트 항목을 추가합니다. 이 항목은 사용자가 sql1.contoso.com에 연결할 때 올바른 호스트에 연결되도록 합니다.

:::image type="content" source="media/sql-server-linux-containers-ad-auth-adutil-tutorial/host-a-record.png" alt-text="호스트 레코드 추가":::

이 자습서에서는 세 개의 VM이 포함된 Azure의 환경을 사용하고 있습니다. 하나의 VM은 도메인 이름이 `contoso.com`인 Windows DC(도메인 컨트롤러) 역할을 합니다. 도메인 컨트롤러의 이름은 `adVM.contoso.com`입니다. 두 번째 머신은 Windows 10 Desktop이 실행되는 `winbox`라는 Windows 머신이며, 클라이언트 머신으로 사용되고 SSMS(SQL Server Management Studio)가 설치되어 있습니다. 세 번째 머신은 `myubuntu`라는 Ubuntu 18.04 LTS 머신이며 SQL Server 컨테이너를 호스트합니다. 모든 머신이 `contoso.com` 도메인에 조인되었습니다. 자세한 내용은 [Linux 호스트의 SQL Server를 Active Directory 도메인에 조인](sql-server-linux-active-directory-join-domain.md)을 참조하세요.

> [!NOTE]
> 이 문서의 뒷부분에서 확인할 수 있듯이 호스트 컨테이너 머신을 반드시 도메인에 조인해야 하는 것은 아닙니다.

## <a name="install-adutil-preview"></a>adutil-preview 설치

Linux 호스트 머신에서 다음 명령을 사용하여 Linux 배포에 따라 adutil-preview를 설치합니다.

> [!NOTE]
> 이 미리 보기 버전에서는 특정 Linux 배포에서 `ACCEPT_EULA` 매개 변수 없이 adutil 설치를 시도하는 경우 설치 환경이 저하될 수 있습니다. 아래의 권장 사항은 `ACCEPT_EULA=Y`로 설정하여 adutil-preview 도구를 설치하는 것입니다. 설치하기 전에 미리 보기 [EULA](https://go.microsoft.com/fwlink/?linkid=2151376)를 읽어볼 수 있습니다. 이 문제를 해결하기 위해 적극적으로 노력하고 있으며 GA 릴리스에서는 해결될 예정입니다.

### <a name="rhel"></a>RHEL

1. Microsoft Red Hat 리포지토리 구성 파일을 다운로드합니다.

    ```bash
    sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/8/prod.repo
    ```

1. 이전 버전의 adutil이 설치되어 있는 경우 이전 adutil 패키지를 제거합니다.

    ```bash
    sudo yum remove adutil
    ```

1. 다음 명령을 실행하여 adutil-preview를 설치합니다. `ACCEPT_EULA=Y`로 설정하면 adutil의 미리 보기 EULA에 동의합니다. EULA는 `/usr/share/adutil/` 경로에 배치됩니다.

    ```bash
    sudo ACCEPT_EULA=Y yum install -y adutil-preview
    ```

### <a name="ubuntu"></a>Ubuntu

1. Microsoft Ubuntu 리포지토리를 등록합니다.

    ```bash
    sudo curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list | sudo tee /etc/apt/sources.list.d/msprod.list
    ```

1. 이전 버전의 adutil을 설치한 경우 다음 명령을 사용하여 이전 adutil 패키지를 제거합니다.

    ```bash
    sudo apt-get remove adutil
    ```

1. 다음 명령을 실행하여 adutil-preview를 설치합니다. `ACCEPT_EULA=Y`로 설정하면 adutil의 미리 보기 EULA에 동의합니다. EULA는 `/usr/share/adutil/` 경로에 배치됩니다.

    ```bash
    sudo ACCEPT_EULA=Y apt-get install -y adutil-preview
    ```

### <a name="sles"></a>SLES

1. Zypper에 Microsoft SQL Server 리포지토리를 추가합니다.

    ```bash
    sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/prod.repo
    ```

1. 이전 버전의 adutil이 설치되어 있는 경우 이전 adutil 패키지를 제거합니다.

    ```bash
    sudo zypper remove adutil
    ```

1. 다음 명령을 실행하여 adutil-preview를 설치합니다. `ACCEPT_EULA=Y`로 설정하면 adutil의 미리 보기 EULA에 동의합니다. EULA는 `/usr/share/adutil/` 경로에 배치됩니다.

    ```bash
    sudo ACCEPT_EULA=Y zypper install -y adutil-preview
    ```

## <a name="creating-the-ad-user-spns-and-sql-server-service-keytab"></a>AD 사용자, SPN 및 SQL Server 서비스 keytab 만들기

SQL Server on Linux 컨테이너 호스트가 도메인에 포함되지 않도록 하고 머신을 도메인에 조인하는 단계를 수행하지 않은 경우 이미 AD 도메인에 포함된 다른 Linux 머신에서 다음 단계를 수행합니다.

 1. adutil 도구를 사용하여 SQL Server의 AD 사용자를 만들고 SPN을 설정합니다.

 2. SQL Server 서비스 keytab 파일을 만들고 구성합니다.

생성된 mssql.keytab 파일을 SQL Server 컨테이너를 실행할 호스트 머신에 복사하고 복사된 mssql.keytab을 사용하도록 컨테이너를 구성합니다. 필요에 따라 SQL Server 컨테이너를 실행할 Linux 호스트를 AD 도메인에 조인하고 동일한 머신에서 다음 단계를 수행할 수도 있습니다.

### <a name="create-an-ad-user-for-sql-server-and-set-the-serviceprincipalname-using-the-adutil-tool"></a>adutil 도구를 사용하여 SQL Server의 AD 사용자 만들기 및 ServicePrincipalName 설정

SQL Server on Linux 컨테이너에서 AD 인증을 사용하도록 설정하려면 AD 도메인에 포함된 Linux 머신에서 아래에 설명된 1-3단계를 실행해야 합니다.

1. `kinit` 명령을 사용하여 Kerberos TGT(Ticket Granting Ticket)를 얻거나 갱신합니다. `kinit` 명령에 권한 있는 계정을 사용합니다. 이 계정에는 도메인에 연결할 수 있는 권한이 있어야 하며 도메인에 계정 및 SPN을 만들 수도 있어야 합니다.

    > [!IMPORTANT]
    > 이 명령을 실행하려면 이전 단계에 표시된 대로 호스트가 도메인에 이미 포함되어 있어야 합니다.

    ```bash
    kinit privilegeduser@DOMAIN.COM
    ```

    예제: 위에 설명된 환경에서 권한 있는 계정은 `amvin@CONTOSO.COM`입니다.

    ```bash
    kinit amvin@CONTOSO.COM
    ```

2. adutil 도구를 사용하여 SQL Server에서 권한 있는 AD 계정으로 사용할 새 사용자를 만듭니다.

   ```bash
   adutil user create --name sqluser -distname CN=sqluser,CN=Users,DC=CONTOSO,DC=COM --password 'P@ssw0rd'
   ```

    > [!NOTE]
    > 암호는 다음 세 가지 방법 중 하나로 지정할 수 있습니다.
    >
    > - 암호 플래그: --password \<password\>
    > - 환경 변수 - `ADUTIL_ACCOUNT_PWD`
    > - 대화형 입력
    >
    > 암호 입력 방법의 우선 순위는 위에 나열된 옵션의 순서를 따릅니다. 권장되는 옵션은 환경 변수나 대화형 입력을 사용하여 암호를 지정하는 것입니다. 이러한 방법은 암호 플래그에 비해 더 안전하기 때문입니다.

    위에 표시된 대로 고유 이름(`-distname`)을 사용하여 계정의 이름을 지정하거나 OU(조직 구성 단위) 이름을 사용할 수도 있습니다. 둘 다 지정하는 경우 OU 이름(`--ou`)이 고유 이름보다 우선적으로 적용됩니다. 자세한 내용을 보려면 다음 명령을 실행할 수 있습니다.

    ```bash
    adutil user create --help
    ```

3. 위에서 만든 사용자에 대해 SPN을 등록합니다. 외부에서 연결을 표시하려는 방식에 따라 원하는 경우 컨테이너 이름 대신 호스트 머신 이름을 사용할 수 있습니다. 이 자습서에서는 포트 1433 대신 5433을 사용합니다. 이는 컨테이너를 매핑하는 포트입니다. 포트 번호는 다를 수 있습니다.

    ```bash
    adutil spn addauto -n sqluser -s MSSQLSvc -H sql1.contoso.com -p 5433
    ```

    > [!NOTE]
    >
    > - `addauto`는 kinit 계정에 충분한 권한이 제공된 경우 SPN을 자동으로 만듭니다.
    > - `-n`: SPN을 할당할 계정의 이름입니다.
    > - `-s`: SPN을 생성하는 데 사용할 서비스 이름입니다. 이 경우는 SQL Server 서비스에 대한 것이므로 서비스 이름은 MSSQLSvc입니다.
    > - `-H`: SPN을 생성하는 데 사용할 호스트 이름입니다. 지정하지 않으면 로컬 호스트의 FQDN이 사용됩니다. 컨테이너 이름에 대한 FQDN도 지정합니다. 이 경우 컨테이너 이름은 `sql1`이고 FQDN은 `sql1.contoso.com`입니다.
    > - `-p`: SPN을 생성하는 데 사용할 포트입니다. 지정하지 않으면 SPN이 포트 없이 생성됩니다. SQL Server가 기본 포트 1433에서 수신 대기하는 경우에만 SQL 연결이 작동합니다.

### <a name="create-the-sql-server-service-keytab-file"></a>SQL Server 서비스 keytab 파일 만들기

이전에 만든 4개의 SPN 각각에 대한 항목을 포함하는 keytab 파일과 사용자에 대한 keytab 파일을 만듭니다. keytab 파일은 컨테이너에 탑재되므로 호스트의 모든 위치에서 만들 수 있습니다. docker/podman을 사용하여 컨테이너를 배포할 때 결과 keytab이 올바르게 탑재되는 한 이 경로를 안전하게 변경할 수 있습니다.

모든 SPN에 대한 keytab을 만들려면 `createauto` 옵션을 사용할 수 있습니다.

```bash
adutil keytab createauto -k /container/sql1/secrets/mssql.keytab -p 5433 -H sql1.contoso.com --password 'P@ssw0rd' -s MSSQLSvc
```

> [!NOTE]
>
> - `-k`: `mssql.keytab` 파일을 만들 경로입니다. 위의 예제에서 “/container/sql1/secrets” 디렉터리는 이미 호스트에 있어야 합니다.
> - `-p`: SPN을 생성하는 데 사용할 포트입니다. 지정하지 않으면 SPN이 포트 없이 생성됩니다.
> - `-H`: SPN을 생성하는 데 사용할 호스트 이름입니다. 지정하지 않으면 로컬 호스트의 FQDN이 사용됩니다. 컨테이너 이름에 대한 FQDN도 지정합니다. 이 경우 컨테이너 이름은 `sql1`이고 FQDN은 `sql1.contoso.com`입니다.
> - `-s`: SPN을 생성하는 데 사용할 서비스 이름입니다. 이 경우는 SQL Server 서비스에 대한 것이므로 서비스 이름은 MSSQLSvc입니다.
> - `--password`: 앞에서 만든 권한 있는 AD 사용자 계정의 암호입니다.
> - `-e` 또는 `--enctype`: keytab 항목의 암호화 유형입니다. 쉼표로 구분된 값 목록을 사용합니다. 지정하지 않으면 대화형 프롬프트가 표시됩니다.

암호화 유형을 선택하는 옵션이 제공되는 경우 둘 이상의 옵션을 선택할 수 있습니다. 이 예제에서는 `aes256-cts-hmac-sha1-96` 및 `arcfour-hmac`를 선택했습니다. 호스트 및 도메인에서 지원하는 암호화 유형을 선택해야 합니다.

암호화 유형을 비대화형으로 선택하려는 경우 위의 명령에서 -e 인수를 사용하여 원하는 암호화 유형을 지정할 수 있습니다. adutil 명령에 대한 추가 도움말을 보려면 다음 명령을 실행합니다.

```bash
adutil keytab createauto --help
```

> [!NOTE]
> `arcfour-hmac`는 약한 암호화이며 프로덕션 환경에서 사용하도록 권장되는 암호화 유형은 아닙니다.

사용자에 대한 keytab을 만드는 명령은 다음과 같습니다.

```bash
adutil keytab create -k /container/sql1/secrets/mssql.keytab -p sqluser --password 'P@ssw0rd!'
```

> [!NOTE]
>
> - `-k`: `mssql.keytab` 파일을 만들 경로입니다. 위의 예제에서 “/container/sql1/secrets” 디렉터리는 이미 호스트에 있어야 합니다.
> - `-p`: keytab에 추가할 사용자입니다.

adutil keytab create/autocreate는 이전 파일을 덮어쓰지 않으며 이미 있는 파일에 추가됩니다.

컨테이너를 배포할 때 생성된 keytab에 올바른 권한이 설정되어 있는지 확인합니다.

```bash
chmod 440 /container/sql1/secrets/mssql.keytab
```

> [!NOTE]
> 이때 mssql.keytab을 현재 Linux 호스트에서 SQL Server 컨테이너를 배포할 Linux 호스트로 복사하고 SQL Server 컨테이너를 실행할 Linux 호스트에서 나머지 단계를 수행할 수 있습니다. SQL 컨테이너가 배포될 동일한 Linux 호스트에서 위의 단계를 수행한 경우 동일한 호스트에서 다음 단계도 수행합니다.

## <a name="create-the-config-files-to-be-used-by-the-sql-server-container"></a>SQL Server 컨테이너에서 사용할 구성 파일 만들기

1. AD에 대한 설정을 사용하여 `mssql.conf` 파일을 만듭니다. 이 파일은 호스트의 어디에나 만들 수 있으며 docker run 명령을 실행하는 동안 올바르게 탑재해야 합니다. 이 예제에서는 이 `mssql.conf` 파일을 컨테이너 디렉터리인 `/container/sql1 ` 아래에 배치했습니다. `mssql.conf`의 내용은 다음과 같습니다.

    ```output
    [network]
    privilegedadaccount = sqluser
    kerberoskeytabfile = /var/opt/mssql/secrets/mssql.keytab
    ```

    > [!NOTE]
    >
    > - `privilagedadaccount`: AD 인증에 사용할 권한을 가진 AD 사용자입니다.
    > - `kerberoskeytabfile`: mssql.keytab 파일이 배치될 컨테이너의 경로입니다.

1. krb5.conf 파일을 만듭니다. 샘플은 다음과 같이 표시됩니다. 이러한 파일에서는 대/소문자 구분이 중요합니다.

    ```output
    [libdefaults]
    default_realm = DOMAIN.COM

    [realms]
     CONTOSO.COM = {
         kdc = adVM.contoso.com
         admin_server = adVM.contoso.com
         default_domain = CONTOSO.COM
     }

    [domain_realm]
     .contoso.com = CONTOSO.COM
     contoso.com = CONTOSO.COM


1. Copy all files, `mssql.conf`, `krb5.conf`, `mssql.keytab` to a location that will be mounted to the SQL Server container. In this example, these files are placed on the host at the following locations: `mssql.conf` and `krb5.conf` at `/container/sql1/`. `mssql.keytab` is placed at the location `/container/sql1/secrets/`.

1. Make sure there's enough permission on these folders for the user running the docker/podman command. When the container starts, the user needs access to the folder path created. In this example, we provided the below permissions given to the folder path:

    ```bash
    sudo chmod 755 /container/sql1/
    ```

## <a name="mount-the-config-files-and-deploy-the-sql-server-container"></a>구성 파일 탑재 및 SQL Server 컨테이너 배포

SQL Server 컨테이너를 실행하고 다음과 같이 이전에 만든 올바른 AD 구성 파일을 탑재합니다.

```bash
sudo docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=\<YourStrong@Passw0rd\>" \
-p 5433:1433 --name sql1 \
-v /container/sql1:/var/opt/mssql \
-v /container/sql1/krb5.conf:/etc/krb5.conf \
-d mcr.microsoft.com/mssql/server:2019-latest
```

> [!NOTE]
> SELinux 사용 호스트와 같은 LSM(Linux 보안 모듈)에서 컨테이너를 실행하는 경우 비공유 프라이빗 레이블로 콘텐츠의 레이블을 지정하도록 docker에 알려 주는 `Z` 옵션을 사용하여 볼륨을 탑재해야 합니다. 자세한 내용은 [configure the SE Linux label](https://docs.docker.com/storage/bind-mounts/#configure-the-selinux-label)(SE Linux 레이블 구성)을 참조하세요.

이 예제에는 다음 명령이 포함됩니다.

```bash
sudo docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=P@ssw0rd" -p 5433:1433 --name sql1 \
-v /container/sql1:/var/opt/mssql/ \
-v /container/sql1/krb5.conf:/etc/krb5.conf \
--dns-search contoso.com \
--dns 10.0.0.4 \
--add-host adVM.contoso.com:10.0.0.4 \
--add-host contoso.com:10.0.0.4 \
--add-host contoso:10.0.0.4 \
-d mcr.microsoft.com/mssql/server:2019-latest
```

> [!NOTE]
>
> - `mssql.conf` 및 `krb5.conf` 파일은 호스트 파일 경로 `/container/sql1`에 있습니다.
> - 생성된 `mssql.keytab`은 호스트 파일 경로 `/container/sql1/secrets`에 있습니다.
> - 호스트 머신이 Azure에 있기 때문에 AD 세부 정보를 동일한 순서로 docker run 명령에 추가해야 합니다. 이 예제에서 도메인 컨트롤러 `adVM`은 `contoso.com` 도메인에 있으며 IP 주소는 `10.0.0.4`입니다. 도메인 컨트롤러는 DNS 및 KDC를 실행합니다.

## <a name="create-ad-based-sql-server-logins-in-transact-sql"></a>Transact-SQL에서 AD 기반 SQL Server 로그인 만들기

SQL 컨테이너에 연결하고 다음 명령을 실행하여 로그인을 만들고 해당 로그인이 나열되는지 확인합니다. 이 명령은 SSMS, ADS(Azure Data Studio) 또는 다른 모든 CLI(명령줄 인터페이스) 도구를 실행하는 클라이언트 머신(Windows 또는 Linux)에서 실행할 수 있습니다.

```sql
create login [contoso\amvin] From Windows
SELECT name FROM sys.server_principals;
```

## <a name="connect-to-sql-server-using-ad-authentication"></a>AD 인증을 사용하여 SQL Server에 연결

[SSMS](../ssms/download-sql-server-management-studio-ssms.md) 또는 [ADS](../azure-data-studio/download-azure-data-studio.md)를 사용하여 연결하려면 SQL Server 이름(이름은 컨테이너 이름 또는 호스트 이름일 수 있음) 및 포트 번호를 사용하는 Windows 자격 증명을 사용하여 SQL Server에 로그인합니다. 이 예제에서 서버 이름은 `sql1.contoso.com, 5433`입니다.

[sqlcmd](../tools/sqlcmd-utility.md)와 같은 도구를 사용하여 컨테이너의 SQL Server에 연결할 수도 있습니다.

```bash
sqlcmd -E -S 'sql1.contoso.com, 5433'
```

## <a name="next-steps"></a>다음 단계

- [빠른 시작: Docker를 사용하여 SQL Server 컨테이너 이미지 실행](quickstart-install-connect-docker.md)
- [Linux 호스트의 SQL Server를 Active Directory 도메인에 가입](sql-server-linux-active-directory-auth-overview.md)
