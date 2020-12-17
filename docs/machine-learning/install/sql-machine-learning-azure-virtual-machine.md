---
title: Azure 가상 머신에 설치
description: Azure 클라우드의 SQL Server Machine Learning Services에서 Python과 R 데이터 과학 및 기계 학습 솔루션을 실행합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 01/02/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15'
ms.openlocfilehash: e8eb32776aa72095c03305d4eb31cf5bb220ebe4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471244"
---
# <a name="install-sql-server-machine-learning-services-with-python-and-r-on-an-azure-virtual-machine"></a>Azure 가상 머신에 Python과 R을 지원하는 SQL Server Machine Learning Services 설치
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

Azure 가상 머신에 Python과 R을 지원하는 SQL Server Machine Learning Services를 설치하는 방법을 알아봅니다. 이렇게 하면 Machine Learning Services에 설치 및 구성 작업을 수행할 필요가 없습니다.

다음 단계를 수행하세요.

1. Azure에서 SQL Server 가상 머신 프로비전
1. 방화벽 차단 해제
1. 원격 클라이언트에 대한 ODBC 콜백 사용
1. 네트워크 프로토콜 추가

## <a name="provision-sql-server-virtual-machine-in-azure"></a>Azure에서 SQL Server 가상 머신 프로비전

단계별 지침은 [Azure Portal에서 Windows SQL Server 가상 머신을 프로비저닝하는 방법](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision)을 참조하세요. 

[SQL 서버 설정 구성](/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings) 단계는 인스턴스에 Machine Learning Services를 추가하는 단계입니다.

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>방화벽 차단 해제

기본적으로 Azure 가상 머신의 방화벽에는 로컬 사용자 계정에 대한 네트워크 액세스를 차단하는 규칙이 포함됩니다.

원격 데이터 과학 클라이언트에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 액세스할 수 있도록 하려면 이 규칙을 비활성화해야 합니다.  그렇지 않으면 가상 머신의 작업 영역을 사용하는 컴퓨팅 컨텍스트에서 기계 학습 코드를 실행할 수 없습니다.

원격 데이터 과학 클라이언트에서 액세스를 활성화하려면 다음을 수행합니다.

1. 가상 머신에서 고급 보안이 포함된 Windows 방화벽을 엽니다.
2. **아웃바운드 규칙** 을 선택합니다.
3. 다음 규칙을 사용하지 않도록 설정합니다.
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>원격 클라이언트에 대한 ODBC 콜백 사용

서버를 호출하는 클라이언트가 ODBC 쿼리를 기계 학습 솔루션의 일부로 실행하게 하려는 경우 원격 클라이언트 대신 실행 패드가 ODBC 호출을 실행할 수 있는지 확인해야 합니다. 

이 작업을 하려면 실행 패드에서 사용되는 SQL 작업자 계정이 인스턴스에 로그인하도록 허용해야 합니다. 자세한 내용은 [데이터베이스 사용자로 SQLRUserGroup 추가](../security/create-a-login-for-sqlrusergroup.md)를 참조하세요.

<a name="network"></a>

## <a name="add-network-protocols"></a>네트워크 프로토콜 추가

+ 명명된 파이프 사용
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]는 클라이언트와 서버 컴퓨터 간의 연결 및 일부 인터넷 연결을 위해 명명된 파이프 프로토콜을 사용합니다. 명명된 파이프를 사용하지 않는 경우 Azure 가상 머신 및 서버에 연결된 데이터 과학 클라이언트에서 둘 다 명명된 파이프를 설치하고 사용하도록 설정해야 합니다.
  
+ TCP/IP 사용

  루프백 연결에는 TCP/IP가 필요합니다. "DBNETLIB; SQL Server가 없거나 액세스가 거부되었습니다" 오류가 발생하면 인스턴스를 지원하는 가상 머신에서 TCP/IP를 사용하도록 설정합니다.