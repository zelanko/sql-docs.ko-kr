---
title: adutil을 사용하여 SQL Server on Linux에서 Active Directory 인증 구성
description: adutil을 사용하여 SQL Server on Linux에서 Active Directory 인증을 구성하는 방법에 대한 단계별 지침
author: amvin87
ms.author: amitkh
ms.reviewer: vanto
ms.date: 12/10/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: linux
moniker: '>= sql-server-linux-2017 || >= sql-server-2017 || =sqlallproducts-allversions'
ms.openlocfilehash: 462c48c7d0ade07c62a154927c352962f454cc46
ms.sourcegitcommit: 18e2f0706e03d0b2b6324845244fbafaa077a8dd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97103302"
---
# <a name="tutorial-configure-active-directory-authentication-with-sql-server-on-linux-using-adutil"></a>자습서: adutil을 사용하여 SQL Server on Linux에서 Active Directory 인증 구성

> [!NOTE]
> **adutil** 은 현재 **퍼블릭 미리 보기** 로 제공됩니다.

이 자습서에서는 adutil을 사용하여 SQL Server on Linux에 대해 AD(Active Directory) 인증을 구성하는 방법을 설명합니다. ktpass를 사용하여 AD 인증을 구성하는 다른 방법은 [자습서: Linux에서 SQL Server와 Active Directory 인증 사용](sql-server-linux-active-directory-authentication.md)을 참조하세요.

이 자습서는 다음 작업으로 구성됩니다.

> [!div class="checklist"]
> - adutil-preview 설치
> - AD 도메인에 Linux 머신 조인
> - adutil 도구를 사용하여 SQL Server의 AD 사용자 만들기 및 SPN(ServicePrincipalName) 설정
> - SQL Server 서비스 keytab 파일 만들기
> - keytab 파일을 사용하도록 SQL Server 구성
> - Transact-SQL을 사용하여 AD 기반 SQL Server 로그인 만들기
> - AD 인증을 사용하여 SQL Server에 연결

## <a name="prerequisites"></a>필수 구성 요소

AD 인증을 구성하려면 다음 항목이 필요합니다.

- 네트워크에 AD 도메인 컨트롤러(Windows)가 있음.
- Linux 호스트 머신에 adutil-preview 도구 설치. adutil-preview 도구를 설치하기 위해 실행 중인 Linux 배포에 따라 아래의 섹션을 수행합니다.

## <a name="install-adutil-preview"></a>adutil-preview 설치

Linux 호스트 머신에서 다음 명령을 사용하여 adutil-preview를 설치합니다.

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

1. 다음 명령을 실행하여 adutil-preview를 설치합니다. `ACCEPT_EULA=Y`로 설정하면 adutil의 미리 보기 EULA에 동의합니다. EULA는 ‘/usr/share/adutil/’ 경로에 배치됩니다.

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

1. 다음 명령을 실행하여 adutil-preview를 설치합니다. `ACCEPT_EULA=Y`로 설정하면 adutil의 미리 보기 EULA에 동의합니다. EULA는 ‘/usr/share/adutil/’ 경로에 배치됩니다.

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

1. 다음 명령을 실행하여 adutil-preview를 설치합니다. `ACCEPT_EULA=Y`로 설정하면 adutil의 미리 보기 EULA에 동의합니다. EULA는 ‘/usr/share/adutil/’ 경로에 배치됩니다.

    ```bash
    sudo ACCEPT_EULA=Y zypper install -y adutil-preview
    ```

## <a name="domain-machine-preparation"></a>도메인 머신 준비

Linux 호스트 IP 주소에 대해 Active Directory에서 추가된 전달 호스트(A) 항목이 있는지 확인합니다. 이 자습서에서 `myubuntu` 호스트 머신의 IP 주소는 `10.0.0.10`입니다. 다음과 같이 Active Directory에서 전달 호스트 항목을 추가합니다. 이 항목은 사용자가 myubuntu.contoso.com에 연결할 때 올바른 호스트에 연결되도록 합니다.

:::image type="content" source="media/sql-server-linux-ad-auth-adutil-tutorial/host-a-record.png" alt-text="호스트 레코드 추가":::

이 자습서에서는 세 개의 VM이 포함된 Azure의 환경을 사용하고 있습니다. 하나의 VM은 도메인 이름이 `contoso.com`인 Windows DC(도메인 컨트롤러) 역할을 합니다. 도메인 컨트롤러의 이름은 `adVM.contoso.com`입니다. 두 번째 머신은 Windows 10 Desktop이 실행되는 `winbox`라는 Windows 머신이며, 클라이언트 머신으로 사용되고 SSMS(SQL Server Management Studio)가 설치되어 있습니다. 세 번째 머신은 `myubuntu`라는 Ubuntu 18.04 LTS 머신이며 SQL Server를 호스트합니다.

## <a name="join-the-linux-host-machine-to-your-ad-domain"></a>AD 도메인에 Linux 호스트 머신 조인

SQL Server Linux 호스트를 Active Directory 도메인 컨트롤러에 연결합니다. Active Directory 도메인을 가입시키는 방법에 대한 자세한 내용은 [Linux 호스트의 SQL Server를 Active Directory 도메인에 가입](sql-server-linux-active-directory-join-domain.md)을 참조하세요.

## <a name="create-an-ad-user-for-sql-server-and-set-the-serviceprincipalname-spn-using-the-adutil-tool"></a>adutil 도구를 사용하여 SQL Server의 AD 사용자 만들기 및 SPN(ServicePrincipalName) 설정

1. `kinit` 명령을 사용하여 Kerberos TGT(Ticket Granting Ticket)를 얻거나 갱신합니다. `kinit` 명령에 권한 있는 계정을 사용합니다. 이 계정에는 도메인에 연결할 수 있는 권한이 있어야 하며 도메인에 계정 및 SPN을 만들 수도 있어야 합니다.

    > [!IMPORTANT]
    > 이 명령을 실행하려면 이전 단계에 표시된 대로 호스트 머신이 도메인에 이미 포함되어 있어야 합니다.

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

3. 위에서 만든 사용자에 대해 SPN을 등록합니다. 머신 FQDN을 사용합니다. 이 자습서에서는 SQL Server의 기본 포트인 1433을 사용합니다. 포트 번호는 다를 수 있습니다.

    ```bash
    adutil spn addauto -n sqluser -s MSSQLSvc -H myubuntu.contoso.com -p 1433
    ```

    > [!NOTE]
    >
    > - `addauto`는 kinit 계정에 충분한 권한이 제공된 경우 SPN을 자동으로 만듭니다.
    > - `-n`: SPN을 할당할 계정의 이름입니다.
    > - `-s`: SPN을 생성하는 데 사용할 서비스 이름입니다. 이 경우는 SQL Server 서비스에 대한 것이므로 서비스 이름은 `MSSQLSvc`입니다.
    > - `-H`: SPN을 생성하는 데 사용할 호스트 이름입니다. 지정하지 않으면 로컬 호스트의 FQDN이 사용됩니다. 이 경우 호스트 이름은 `myubuntu`이고 FQDN은 `myubuntu.contoso.com`입니다.
    > - `-p`: SPN을 생성하는 데 사용할 포트입니다. 지정하지 않으면 SPN이 포트 없이 생성됩니다. SQL Server가 기본 포트 1433에서 수신 대기하는 경우에만 SQL 연결이 작동합니다.

## <a name="create-the-sql-server-service-keytab-file"></a>SQL Server 서비스 keytab 파일 만들기

이전에 만든 4개의 SPN 각각에 대한 항목을 포함하는 keytab 파일과 사용자에 대한 keytab 파일을 만듭니다.

```bash
adutil keytab createauto -k /var/opt/mssql/secrets/mssql.keytab -p 1433 -H myubuntu.contoso.com --password 'P@ssw0rd' -s MSSQLSvc 
```

> [!NOTE]
>
> - `-k`: `mssql.keytab` 파일을 만들 경로입니다. 위의 예제에서 `/var/opt/mssql/secrets/` 디렉터리는 이미 호스트에 있어야 합니다.
> - `-p`: SPN을 생성하는 데 사용할 포트입니다. 지정하지 않으면 SPN이 포트 없이 생성됩니다.
> - `-H`: SPN을 생성하는 데 사용할 호스트 이름입니다. 지정하지 않으면 로컬 호스트의 FQDN이 사용됩니다. 이 경우 호스트 이름은 `myubuntu`이고 FQDN은 `myubuntu.contoso.com`입니다.
> - `-s`: SPN을 생성하는 데 사용할 서비스 이름입니다. 이 경우는 SQL Server 서비스에 대한 것이므로 서비스 이름은 `MSSQLSvc`입니다.
> - `--password`: 앞에서 만든 권한 있는 AD 사용자 계정의 암호입니다.
> - `-e` 또는 `--enctype`: keytab 항목의 암호화 유형입니다. 쉼표로 구분된 값 목록을 사용합니다. 지정하지 않으면 대화형 프롬프트가 표시됩니다.

암호화 유형을 선택하는 옵션이 제공되는 경우 둘 이상의 옵션을 선택할 수 있습니다. 이 예제에서는 `aes256-cts-hmac-sha1-96` 및 `arcfour-hmac`를 선택했습니다. 호스트 및 도메인에서 지원하는 암호화 유형을 선택해야 합니다.

암호화 유형을 비대화형으로 선택하려는 경우 위의 명령에서 -e 인수를 사용하여 원하는 암호화 유형을 지정할 수 있습니다. adutil 명령에 대한 추가 도움말을 보려면 다음 명령을 실행합니다.

```bash
adutil keytab createauto --help
```

> [!NOTE]
> `arcfour-hmac`는 약한 암호화이며 프로덕션 환경에서 사용하도록 권장되는 암호화 유형은 아닙니다.

SQL Server에서 AD에 연결하는 데 사용할 사용자 이름 및 암호에 대한 항목을 keytab에 추가합니다.

```bash
adutil keytab create -k /var/opt/mssql/secrets/mssql.keytab -p sqluser --password 'P@ssw0rd!'
```

> [!NOTE]
>
> - `-k`: `mssql.keytab` 파일을 만들 경로입니다.
> - `-p`: keytab에 추가할 사용자입니다.

adutil keytab create/autocreate는 이전 파일을 덮어쓰지 않으며 이미 있는 파일에 추가됩니다.

생성된 keytab은 `mssql` 사용자가 소유하고 `mssql` 사용자만 파일에 대한 읽기/쓰기 권한을 갖는지 확인합니다. 다음과 같이 `chown` 및 `chmod` 명령을 실행할 수 있습니다.

```bash
chown mssql. /var/opt/mssql/secrets/mssql.keytab
chmod 440 /var/opt/mssql/secrets/mssql.keytab
```

## <a name="configure-sql-server-to-use-the-keytab"></a>keytab을 사용하도록 SQL Server 구성

다음 명령을 실행하여 이전 단계에서 만든 keytab을 사용하도록 SQL Server를 구성하고 권한 있는 AD 계정을 위에서 만든 사용자로 설정합니다. 이 예제에서 사용자 이름은 `sqluser`입니다.

```bash
/opt/mssql/bin/mssql-conf set network.kerberoskeytabfile /var/opt/mssql/secrets/mssql.keytab
/opt/mssql/bin/mssql-conf set network.privilegedadaccount sqluser
```

## <a name="restart-sql-server"></a>SQL Server 다시 시작

다음 명령을 실행하여 SQL Server 서비스를 다시 시작합니다.

```bash
sudo systemctl restart mssql-server
```

## <a name="create-ad-based-sql-server-logins-in-transact-sql"></a>Transact-SQL에서 AD 기반 SQL Server 로그인 만들기

SQL Server에 연결하고 다음 명령을 실행하여 로그인을 만들고 해당 로그인이 나열되는지 확인합니다.

```sql
create login [contoso\amvin] From Windows
SELECT name FROM sys.server_principals;
```

## <a name="connect-to-sql-server-using-ad-authentication"></a>AD 인증을 사용하여 SQL Server에 연결

[SSMS](../ssms/download-sql-server-management-studio-ssms.md) 또는 [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md)를 사용하여 연결하려면 Windows 자격 증명을 사용하여 SQL Server에 로그인합니다.

[sqlcmd](../tools/sqlcmd-utility.md)와 같은 도구를 사용하여 Windows 인증을 사용하는 SQL Server에 연결할 수도 있습니다.

```bash
sqlcmd -E -S 'myubuntu.contoso.com'
```

## <a name="next-steps"></a>다음 단계

- [Linux 호스트의 SQL Server를 Active Directory 도메인에 가입](sql-server-linux-active-directory-auth-overview.md)
- SQL Server on Linux 컨테이너에서 AD 인증을 구성하는 방법에 관심이 있는 경우 [SQL Server on Linux 컨테이너에서 Active Directory 인증 구성](sql-server-linux-containers-ad-auth-adutil-tutorial.md) 참조
