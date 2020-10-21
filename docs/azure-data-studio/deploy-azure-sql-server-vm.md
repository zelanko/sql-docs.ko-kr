---
title: Azure Virtual Machine에 SQL Server 배포
description: 이 자습서에서는 Azure Virtual Machines에 SQL Server를 만드는 방법을 보여 줍니다.
author: ninarn
ms.author: ninarn
ms.reviewer: alayu, maghan
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 453ec8226b018b1d5d756ba96ac174823657c5dd
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92060917"
---
# <a name="create-sql-server-on-azure-virtual-machines-using-azure-data-studio"></a>Azure Data Studio를 사용하여 Azure Virtual Machines에서 SQL Server 만들기

배포 마법사 및 Notebook을 통해 Azure Data Studio를 사용하여 SQL VM(가상 머신)을 만들 수 있습니다.

## <a name="pre-requisites"></a>필수 구성 요소

- [Azure Data Studio](download-azure-data-studio.md)가 설치되어 있음
- 활성 Azure 계정 및 구독. 아직 없는 경우 [체험 계정](https://azure.microsoft.com/free/)을 만들 수 있습니다.

## <a name="use-the-deployment-wizard"></a>배포 마법사 사용

간단한 UI 환경에서 필요한 설정을 안내하는 배포 마법사를 사용하려면 다음 단계를 수행합니다.

먼저 배포 마법사에서 Azure SQL VM을 찾아 선택합니다.

1. Azure Data Studio에서 왼쪽 탐색에 있는 연결 뷰렛을 선택합니다.

2. 연결 패널 맨 위에 있는 **...** 단추를 선택하고 **새 배포**를 선택합니다.

3. 배포 마법사에서 **Azure SQL VM** 타일을 선택하고 동의함 확인란을 선택합니다.

4. 메시지가 표시되면 필요한 도구를 설치한 다음, 맨 아래에 있는 **선택** 단추를 선택합니다.

Azure SQL VM 마법사에서 필수 매개 변수를 모두 입력합니다.

1. 아직 Azure 계정에 로그인하지 않은 경우 지금 로그인합니다. 이 마법사 페이지에 이슈가 있는 경우 연결을 새로 고칠 수 있습니다.

2. 원하는 구독, 리소스 그룹, 지역을 선택합니다. 그런 후 **다음**을 선택합니다.

3. 고유한 가상 머신 이름과 사용자 이름 및 암호 자격 증명을 입력합니다.

4. 원하는 이미지, SKU, 버전을 선택한 다음, 원하는 VM 크기를 선택합니다. [사용 가능한 VM 크기](https://docs.microsoft.com/azure/virtual-machines/sizes)에 대해 자세히 알아보면 선택하는 데 도움이 될 수 있습니다. 그런 후 **다음**을 선택합니다.

5. 드롭다운에서 기존 가상 네트워크를 선택하거나, **새 가상 네트워크** 확인란을 선택하여 새 가상 네트워크의 이름을 입력합니다.

6. 동일한 방법으로 서브넷 및 공용 IP 주소를 선택하거나 만듭니다.

7. RDP(원격 데스크톱)를 통해 VM에 연결하려는 경우 **RDP 인바운드 포트 사용** 확인란을 선택합니다. 그런 후 **다음**을 선택합니다.

8. 기본 SQL Server 설정을 입력합니다. 이 환경을 테스트하기 위한 권장 사항은 SQL 연결을 **퍼블릭(인터넷)** 으로 설정하고, 포트 1433을 입력한 다음, 기본 설정 사용자 이름 및 암호로 SQL 인증을 사용하도록 설정하는 것입니다. 그런 후 **다음**을 선택합니다.

9. 입력한 매개 변수를 검토하고 **Notebook으로 스크립트**를 선택합니다.

Notebook이 열리면 콘텐츠와 코드를 검토하고 원하는 경우 변경할 수 있습니다. 그러나 유효성 검사 오류가 발생할 수 있으므로 변경하지 않는 것이 좋습니다.

마지막 단계는 **모두 실행**을 선택하여 Notebook의 모든 셀을 실행하는 것입니다. 이 작업이 완료되면 다음 항목이 완전히 생성되어 실행됩니다.

- Azure 가상 머신
- SQL 가상 머신
- 가상 네트워크, 서브넷, 공용 IP 주소
- 네트워크 보안 그룹 및 네트워크 인터페이스
- VM RDP에 대한 액세스 권한
- 다양한 SQL Server 관리 효율성 기능에 액세스하여 백업 일정, 패치 일정, SQL Server 버전 및 라이선스, 스토리지 성능 구성 등을 쉽게 제어할 수 있습니다.

## <a name="next-steps"></a>다음 단계

데이터를 새 SQL VM으로 마이그레이션하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

> [!div class="nextstepaction"]
> [SQL VM에 데이터베이스 마이그레이션](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/migrate-to-vm-from-sql-server)

Azure에서 SQL Server를 사용하는 방법에 대한 기타 정보는 [Azure Virtual Machines의 SQL Server](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/sql-server-on-azure-vm-iaas-what-is-overview) 및 [질문과 대답](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/frequently-asked-questions-faq)을 참조하세요.
