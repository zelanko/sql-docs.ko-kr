---
title: SQL Server 로그인 대화 상자(OLE DB) | Microsoft Docs
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
ms.openlocfilehash: a05dc6221aee2dbd3b7b97c28e7bfecc9ce325bf
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85987237"
---
# <a name="sql-server-login-dialog-box"></a>SQL Server 로그인 대화 상자
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

사용자가 충분한 정보를 지정하지 않고 연결을 시도하면 OLE DB 드라이버가 **SQL Server 로그인** 대화 상자를 표시합니다.

> [!NOTE]  
> SQL Server 로그인 대화 상자 동작은 `DBPROP_INIT_PROMPT` 초기화 속성에 의해 제어됩니다. 자세한 내용은 다음을 참조하세요.
> - [초기화 및 권한 부여 속성](../ole-db-data-source-objects/initialization-and-authorization-properties.md)
> - [OLE DB 프로그래머 가이드](https://go.microsoft.com/fwlink/?linkid=2067702)

![SQL Server 로그인 대화 상자의 스크린샷](../media/sql-server-login-dialog.png)

## <a name="options"></a>옵션
|옵션|Description|
|---   |---        |
|서버|네트워크에서 SQL Server 인스턴스의 이름입니다. 목록에서 서버\인스턴스 이름을 선택하거나 **서버** 상자에 서버\인스턴스 이름을 입력합니다. 필요한 경우 **SQL Server 구성 관리자**를 사용하여 클라이언트 컴퓨터에서 서버 별칭을 만들고 **서버** 상자에 이 이름을 입력할 수 있습니다. <br/><br/>SQL Server와 동일한 컴퓨터를 사용하는 경우에는 "(로컬)"을 입력할 수 있습니다. 그러면 네트워크에 연결되지 않은 SQL Server 버전을 실행하는 경우에도 SQL Server의 로컬 인스턴스에 연결할 수 있습니다.<br/><br/>여러 네트워크 유형의 서버 이름에 대한 자세한 내용은 [SQL Server 설치](https://go.microsoft.com/fwlink/?linkid=2067541)를 참조하세요.|
|인증 모드|드롭다운 목록에서 다음 인증 옵션을 선택할 수 있습니다.<br/><ul><li>`Windows Authentication:` 현재 로그인한 사용자의 Windows 계정 자격 증명을 사용하는 SQL Server 인증입니다.</li><li>`SQL Server Authentication:` 로그인 ID 및 암호를 사용하는 인증입니다.</li><li>`Active Directory - Integrated:` Azure Active Directory ID를 사용하는 통합 인증입니다. 이 모드는 SQL Server에 대한 Windows 인증에도 사용할 수 있습니다.</li><li>`Active Directory - Password:` Azure Active Directory ID를 사용하는 사용자 ID 및 암호 인증입니다.</li><li>`Active Directory - Universal with MFA support:` Azure Active Directory ID를 사용하는 대화형 인증입니다. 이 모드는 Azure MFA(다단계 인증)를 지원합니다.</li></ul>|
|서버 SPN|트러스트된 연결을 사용하면 서버에 대한 SPN(서비스 사용자 이름)을 지정할 수 있습니다.|
|로그인 ID|연결에 사용할 로그인 ID를 지정합니다. 로그인 ID 텍스트 상자는 `Authentication Mode`가 `SQL Server Authentication`, `Active Directory - Password` 또는 `Active Directory - Universal with MFA support`로 설정된 경우에만 사용할 수 있습니다.|
|암호|연결에 사용되는 암호를 지정합니다. 암호 텍스트 상자는 `Authentication Mode`가 `SQL Server Authentication` 또는 `Active Directory - Password`로 설정된 경우에만 사용할 수 있습니다.|
|옵션|**옵션** 그룹을 표시하거나 숨깁니다. **옵션** 단추는 **서버**에 값이 있는 경우 사용할 수 있습니다.|
|암호 변경|이 확인란을 선택하면 **새 암호** 및 **새 암호 확인** 텍스트 상자를 사용할 수 있습니다.|
|새 암호|새 암호를 지정합니다.|
|새 암호 확인|확인을 위해 새 암호를 다시 한 번 지정합니다.|
|데이터베이스|연결에 사용할 기본 데이터베이스를 선택하거나 입력합니다. 이 설정은 서버의 로그인에 지정된 기본 데이터베이스를 덮어씁니다. 데이터베이스를 지정하지 않으면 서버의 로그인에 지정된 기본 데이터베이스가 연결에 사용됩니다.|
|미러 서버|미러되는 데이터베이스의 장애 조치(failover) 파트너 이름을 지정합니다.|
|미러 SPN|필요에 따라 미러 서버에 대한 SPN을 지정할 수 있습니다. 미러 서버에 대한 SPN은 클라이언트와 서버 간의 상호 인증에 사용됩니다.|
|언어|SQL Server 시스템 메시지에 사용할 국가별 언어를 지정합니다. SQL Server를 실행하는 컴퓨터에 해당 언어가 설치되어 있어야 합니다. 이 설정은 서버의 로그인에 지정된 기본 언어를 덮어씁니다. 언어를 지정하지 않으면 서버의 로그인에 지정된 기본 언어가 연결에 사용됩니다.|
|애플리케이션 이름|**sys.sysprocesses**에서 이 연결에 대한 행의 **program_name** 열에 저장할 애플리케이션 이름을 지정합니다.|
|워크스테이션 ID|**sys.sysprocesses**에서 이 연결에 대한 행의 **hostname** 열에 저장할 워크스테이션 ID를 지정합니다.|
|데이터에 대하여 강력한 암호화 사용|이 확인란을 선택하면 연결을 통해 전달되는 데이터가 암호화됩니다.|
|서버 인증서 신뢰|이 확인란을 선택하면 서버 인증서의 유효성이 검사됩니다. 서버 인증서에는 올바른 서버 호스트 이름이 있어야 하며 신뢰할 수 있는 인증 기관에서 발급한 인증서가 있어야 합니다.|

> [!NOTE]  
> `Windows Authentication` 또는 `SQL Server Authentication` 모드를 사용하는 경우 **서버 인증서 신뢰**는 **데이터에 대해 강력한 암호화 사용** 옵션을 사용하는 경우에만 고려됩니다.

## <a name="next-steps"></a>다음 단계
- OLE DB 드라이버를 사용하여 [Azure Active Directory에 인증](../features/using-azure-active-directory.md)합니다.
- [UDL(유니버설 데이터 링크)](data-link-pages.md)을 사용하여 연결 정보를 설정합니다.