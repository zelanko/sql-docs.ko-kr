---
title: Azure 가상 컴퓨터-SQL Server Machine Learning Services에서 R 언어 및 Python 기능을 설치 합니다.
description: R 및 Python 데이터 과학 및 기계 학습 솔루션은 Azure 클라우드에서 SQL Server 가상 머신에서 실행 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 01fb7962a5be08f40fe1c790b335c24d34979a2a
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67141472"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-on-an-azure-virtual-machine"></a>R 및 Python을 사용 하 여 Azure 가상 머신에 SQL Server Machine Learning Services 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

설치 및 구성 태스크를 제거 하는 Azure에서 SQL Server 가상 컴퓨터에서 Machine Learning 서비스를 사용 하 여 R 및 Python 통합을 설치할 수 있습니다. 가상 머신이 배포 되 면 기능은 사용할 준비가 됩니다.
 
단계별 지침은 [Azure portal에서 Windows SQL Server 가상 컴퓨터를 프로 비전 하는 방법을](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision)합니다.

합니다 [구성할 SQL server 설정](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision#3-configure-sql-server-settings) 단계에 기계 학습을 추가한 것입니다.

<a name="firewall"></a>

## <a name="unblock-the-firewall"></a>방화벽 차단 해제

기본적으로 Azure 가상 컴퓨터의 방화벽이 네트워크 로컬 사용자 계정에 대 한 액세스를 차단 하는 규칙을 포함 합니다.

이 규칙에 액세스할 수 있는지 확인을 사용 하지 않도록 설정 해야 합니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원격 데이터 과학 클라이언트에서 인스턴스.  그렇지 않으면 기계 학습 코드는 가상 머신의 작업 영역을 사용 하는 계산 컨텍스트에서 실행할 수 없습니다.

원격 데이터 과학 클라이언트에서 액세스할 수 있도록 합니다.

1. 가상 머신에서 고급 보안이 포함된 Windows 방화벽을 엽니다.
2. **아웃바운드 규칙**을 선택합니다.
3. 다음 규칙을 사용하지 않도록 설정합니다.
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`
  
## <a name="enable-odbc-callbacks-for-remote-clients"></a>원격 클라이언트에 대한 ODBC 콜백 사용

서버를 호출 하는 클라이언트는 기계 학습 솔루션의 일부로 ODBC 쿼리를 실행 해야는 예상 되는 경우 실행 패드는 원격 클라이언트 대신 ODBC 호출을 수행할 수 있는지 확인 해야 합니다. 

이 작업을 하려면 실행 패드에서 사용되는 SQL 작업자 계정이 인스턴스에 로그인하도록 허용해야 합니다. 자세한 내용은 [SQLRUserGroup을 데이터베이스 사용자로 추가](../security/create-a-login-for-sqlrusergroup.md)합니다.

<a name="network"></a>

## <a name="add-network-protocols"></a>네트워크 프로토콜 추가

+ 명명된 파이프 사용
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]는 클라이언트와 서버 컴퓨터 간의 연결 및 일부 인터넷 연결을 위해 명명된 파이프 프로토콜을 사용합니다. 명명된 파이프를 사용하지 않는 경우 Azure 가상 머신 및 서버에 연결된 데이터 과학 클라이언트에서 둘 다 명명된 파이프를 설치하고 사용하도록 설정해야 합니다.
  
+ TCP/IP 사용

  TCP/IP는 루프백 연결에 필요 합니다. "DBNETLIB 오류가 발생할 경우 SQL Server가 없거나 액세스가 거부 되었습니다", 인스턴스를 지 원하는 가상 머신에서 TCP/IP를 설정 합니다.