---
title: SQL Server 2019 on Linux의 새로운 기능
description: 이 문서에서는 SQL Server 2019 on Linux의 새로운 기능을 중점적으로 설명합니다.
author: VanMSFT
ms.author: vanto
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 5183efa51afd89ad82d0cdcb6448996429b81d28
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "72890554"
---
# <a name="whats-new-for-sql-server-2019-on-linux"></a>SQL Server 2019 on Linux의 새로운 기능

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Linux에서 실행되는 SQL Server 2019에 사용할 수 있는 주요 기능 및 서비스에 대해 설명합니다. 패키지 다운로드 및 알려진 문제에 대해서는 [릴리스 정보](sql-server-linux-release-notes-2019.md?view=sql-server-linux-ver15)를 참조하세요.

## <a name="updates"></a>업데이트

SQL Server 2019 on Linux에서 업데이트가 수행되었습니다.

| 새로운 기능 또는 업데이트 | 세부 정보 |
|:-----|:-----|
|복제 지원 |[Linux의 SQL Server 복제 개체](sql-server-linux-replication.md)
|MSDTC(Microsoft Distributed Transaction Coordinator) 지원 |[Linux에서 MSDTC를 구성하는 방법](sql-server-linux-configure-msdtc.md) |
|타사 AD 공급자에 대한 OpenLDAP 지원 |[자습서: Linux에서 SQL Server와 Active Directory 인증 사용](sql-server-linux-active-directory-authentication.md) |
|Linux의 Machine Learning |[Linux에서 Machine Learning 구성](sql-server-linux-setup-machine-learning.md) |
|`tempdb` 개선 사항 | 기본적으로 Linux에 SQL Server를 새로 설치하면 논리적 코어 수(최대 8개 데이터 파일 포함)에 따라 여러 `tempdb` 데이터 파일이 생성됩니다. 이 위치에서 부 버전 또는 주 버전 업그레이드에는 적용되지 않습니다. 각 `tempdb` 파일은 자동 증가 속도가 64MB인 8MB입니다. 이 동작은 Windows의 기본 SQL Server 설치와 유사합니다. |
| Linux의 PolyBase. | Hadoop이 아닌 커넥터에 대한 Linux에 [PolyBase를 설치](../relational-databases/polybase/polybase-linux-setup.md)합니다.<br/><br/>[PolyBase 형식 매핑](../relational-databases/polybase/polybase-type-mapping.md). |
| CDC(변경 데이터 캡처) 지원 | CDC(변경 데이터 캡처)는 이제 SQL Server 2019용 Linux에서 지원됩니다. |
| Microsoft Container Registry | 이제 [Microsoft Container Registry](https://www.ntweekly.com/2019/09/23/microsoft-container-registry-to-replace-docker-hub-for-new-images/)가 Docker Hub 대신 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]를 비롯한 새 공식적인 Microsoft 컨테이너 이미지를 제공합니다. |
| 루트가 아닌 컨테이너 | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]에서는 기본적으로 [!INCLUDE[sql-server](../includes/ssnoversion-md.md)] 프로세스를 루트가 아닌 사용자로 시작하여 더 안전한 컨테이너를 만들 수 있습니다. 자세한 내용은 [루트가 아닌 사용자 권한으로 SQL Server 컨테이너 빌드 및 실행](sql-server-linux-configure-docker.md#buildnonrootcontainer)을 참조하세요. |

## <a name="next-steps"></a>다음 단계

SQL Server on Linux를 설치하려면 다음 자습서 중 하나를 사용합니다.

- [Red Hat Enterprise Linux에 설치](quickstart-install-connect-red-hat.md?view=sql-server-linux-ver15)
- [SUSE Linux Enterprise Server에 설치](quickstart-install-connect-suse.md?view=sql-server-linux-ver15)
- [Ubuntu에 설치](quickstart-install-connect-ubuntu.md?view=sql-server-linux-ver15)
- [Docker에서 실행](quickstart-install-connect-docker.md?view=sql-server-linux-ver15)
- [Azure에서 SQL VM 프로비전](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

질문과 대답은 [SQL Server on Linux FAQ](sql-server-linux-faq.md)를 참조하세요. SQL Server 2019에 도입된 다른 향상된 기능을 보려면 [SQL Server 2019의 새로운 기능](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15)을 참조하세요.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
