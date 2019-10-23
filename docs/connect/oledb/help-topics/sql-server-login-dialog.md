---
title: SQL Server 로그인 대화 상자 (OLE DB) | Microsoft Docs
description: SQL Server 로그인 대화 상자 사용
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: d35c339798b4385cb903d8a4a83f13184bbf4db3
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381754"
---
# <a name="sql-server-login-dialog-box"></a>SQL Server 로그인 대화 상자
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

충분 한 정보를 지정 하지 않고 연결 하려고 하면 OLE DB 드라이버가 **SQL Server 로그인** 대화 상자를 표시 합니다.

> [!NOTE]  
> SQL Server 로그인 대화 상자 동작은 `DBPROP_INIT_PROMPT` 초기화 속성에 의해 제어 됩니다. 참조 항목:
> - [초기화 및 권한 부여 속성](../ole-db-data-source-objects/initialization-and-authorization-properties.md)
> - [OLE DB 프로그래머 가이드](https://go.microsoft.com/fwlink/?linkid=2067702)

![SQL Server 로그인 대화 상자 스크린샷](../media/sql-server-login-dialog.png)

## <a name="options"></a>옵션
|옵션|설명|
|---   |---        |
|서버|네트워크에 SQL Server 인스턴스의 이름입니다. 목록에서 서버\인스턴스 이름을 선택하거나 **서버** 상자에 서버\인스턴스 이름을 입력합니다. 필요한 경우 **SQL Server 구성 관리자**를 사용하여 클라이언트 컴퓨터에서 서버 별칭을 만들고 **서버** 상자에 이 이름을 입력할 수 있습니다. <br/><br/>SQL Server와 동일한 컴퓨터를 사용하는 경우에는 "(로컬)"을 입력할 수 있습니다. 그러면 네트워크에 연결되지 않은 SQL Server 버전을 실행하는 경우에도 SQL Server의 로컬 인스턴스에 연결할 수 있습니다.<br/><br/>여러 네트워크 유형의 서버 이름에 대 한 자세한 내용은 [SQL Server 설치](https://go.microsoft.com/fwlink/?linkid=2067541)를 참조 하세요.|
|인증 모드|드롭다운 목록에서 다음 인증 옵션을 선택할 수 있습니다.<br/><ul><li>현재 로그인 한 사용자의 Windows 계정 자격 증명을 사용 하 여 SQL Server에 대 한 인증을 `Windows Authentication:` 합니다.</li><li>로그인 ID 및 암호를 사용 하 여 인증을 `SQL Server Authentication:` 합니다.</li><li>Azure Active Directory id를 사용 하 여 통합 인증을 `Active Directory - Integrated:` 합니다. 이 모드는 Windows 인증을 SQL Server 하는 데에도 사용할 수 있습니다.</li><li>Azure Active Directory id를 사용 하 여 사용자 ID 및 암호 인증을 `Active Directory - Password:` 합니다.</li><li>Azure Active Directory id를 사용 하 여 대화형 인증을 `Active Directory - Universal with MFA support:` 합니다. 이 모드는 Azure MFA (multi-factor authentication)를 지원 합니다.</li></ul>|
|서버 SPN|트러스트된 연결을 사용하면 서버에 대한 SPN(서비스 사용자 이름)을 지정할 수 있습니다.|
|로그인 ID|연결에 사용할 로그인 ID를 지정 합니다. 로그인 ID 텍스트 상자는 `Authentication Mode` `SQL Server Authentication`, `Active Directory - Password` 또는 `Active Directory - Universal with MFA support`로 설정 된 경우에만 사용할 수 있습니다.|
|암호|연결에 사용 되는 암호를 지정 합니다. 암호 텍스트 상자는 `Authentication Mode` `SQL Server Authentication` 또는 `Active Directory - Password`으로 설정 된 경우에만 사용할 수 있습니다.|
|옵션|**옵션** 그룹을 표시하거나 숨깁니다. **옵션** 단추는 **서버**에 값이 있는 경우 사용할 수 있습니다.|
|암호 변경|이 확인란을 선택 하면 **새 암호** 및 **새 암호 확인** 입력란이 사용 됩니다.|
|새 암호|새 암호를 지정합니다.|
|새 암호 확인|확인을 위해 새 암호를 다시 한 번 지정합니다.|
|데이터베이스|연결에 사용할 기본 데이터베이스를 선택하거나 입력합니다. 이 설정은 서버의 로그인에 지정된 기본 데이터베이스를 덮어씁니다. 데이터베이스를 지정하지 않으면 서버의 로그인에 지정된 기본 데이터베이스가 연결에 사용됩니다.|
|미러 서버|미러되는 데이터베이스의 장애 조치(failover) 파트너 이름을 지정합니다.|
|미러 SPN|필요에 따라 미러 서버에 대한 SPN을 지정할 수 있습니다. 미러 서버에 대한 SPN은 클라이언트와 서버 간의 상호 인증에 사용됩니다.|
|언어|SQL Server 시스템 메시지에 사용할 국가별 언어를 지정합니다. SQL Server를 실행하는 컴퓨터에 해당 언어가 설치되어 있어야 합니다. 이 설정은 서버의 로그인에 지정된 기본 언어를 덮어씁니다. 언어를 지정하지 않으면 서버의 로그인에 지정된 기본 언어가 연결에 사용됩니다.|
|Application Name|**sys.sysprocesses**에서 이 연결에 대한 행의 **program_name** 열에 저장할 애플리케이션 이름을 지정합니다.|
|워크스테이션 ID|**sys.sysprocesses**에서 이 연결에 대한 행의 **hostname** 열에 저장할 워크스테이션 ID를 지정합니다.|
|데이터에 대하여 강력한 암호화 사용|이 확인란을 선택 하면 연결을 통해 전달 되는 데이터가 암호화 됩니다.|
|서버 인증서 신뢰|이 확인란을 선택 하면 서버의 인증서 유효성이 검사 됩니다. 서버 인증서에는 올바른 서버 호스트 이름이 있어야 하며 신뢰할 수 있는 인증 기관에서 발급 한 인증서가 있어야 합니다.|

> [!NOTE]  
> @No__t_0 또는 `SQL Server Authentication` 모드를 사용 하는 경우 **트러스트 서버 인증서** 는 **데이터에 대해 강력한 암호화 사용** 옵션을 사용 하는 경우에만 고려 됩니다.

## <a name="next-steps"></a>다음 단계
- OLE DB 드라이버를 사용 하 여 [Azure Active Directory에 인증](../features/using-azure-active-directory.md) 합니다.
- [유니버설 데이터 링크 (UDL)](data-link-pages.md)를 사용 하 여 연결 정보를 설정 합니다.