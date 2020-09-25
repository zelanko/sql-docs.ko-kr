---
title: Azure Data Studio를 사용하여 Azure SQL Edge 배포
description: Azure Data Studio에서 Azure SQL Edge 인스턴스를 배포하는 방법
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: seodec18
ms.date: 09/22/2020
ms.openlocfilehash: eab4881c53ce26790a78a7da69a4bd48731fecfa
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90990006"
---
# <a name="deploy-azure-sql-edge-with-azure-data-studio-preview"></a>Azure Data Studio를 사용하여 Azure SQL Edge 배포(미리 보기)

[Azure SQL Edge](https://docs.microsoft.com/azure/azure-sql-edge/overview)는 IoT 및 Azure IoT Edge 배포에 최적화된 관계형 데이터베이스 엔진으로, IoT 애플리케이션과 솔루션을 위한 고성능 데이터 스토리지 및 처리 계층을 만드는 기능을 제공합니다. 이 문서에서는 Azure Data Studio를 사용하여 Azure SQL Edge 인스턴스를 배포하는 방법과 배포 마법사에서 지원되는 배포 시나리오를 보여 줍니다.  

Azure Data Studio의 배포 마법사에서 지원되는 시나리오는 다음과 같습니다.

- 로컬 컨테이너 인스턴스
- 원격 컨테이너 인스턴스
- 새 Azure IoT 허브 및 VM
- Azure IoT 허브의 기존 디바이스
- Azure IoT 허브의 여러 디바이스

| 필요한 도구 | `Docker` | `Azure CLI` |
| ------------- | :---: | :---: |
| 로컬 컨테이너 인스턴스 | x | |
| 원격 컨테이너 인스턴스 | | |
| 새 Azure IoT 허브 및 VM | | x |
| Azure IoT 허브의 기존 디바이스 |  | x |
| Azure IoT 허브의 여러 디바이스 |   |  x |

> [!NOTE]
> Azure SQL Edge 배포(미리 보기)는 “Azure SQL Edge 배포 확장”을 통해 사용할 수 있으며 해당 기능은 미리 보기로 제공됩니다. 이 기능을 사용하려면 Azure Data Studio에서 해당 확장을 설치합니다.

Azure Data Studio에서 배포를 시작하려면 **연결** 보기에서 메뉴를 열고 **새 배포...** 옵션을 선택합니다.  모든 Azure SQL Edge 시나리오의 경우 다음 화면에서 **Azure SQL Edge**를 선택하고 **배포 대상** 드롭다운에서 원하는 시나리오를 선택합니다. 배포 마법사는 배포를 완료하기 위해 실행할 수 있는 TSQL Notebook을 생성합니다. SQL 관리자 암호를 비롯한 연결 정보는 Notebook에 기본적으로 포함되어 있습니다.

![배포 개요](media/deploy-azure-sql-edge/deploy-overview.png)

## <a name="local-container-instance"></a>로컬 컨테이너 인스턴스

컨테이너 이름, `sa` 사용자 암호, Azure SQL Edge 연결에 사용할 호스트 포트를 지정하여 localhost의 Docker 컨테이너에 Azure SQL Edge를 배포할 수 있습니다.  배포를 완료한 후 Notebook 맨 아래에 있는 여러 링크를 사용하여 추가 작업을 수행할 수 있습니다.

- **Azure SQL Edge 인스턴스에 연결하려면 여기를 선택**: Azure Data Studio에서 새 Azure SQL Edge 인스턴스에 대한 연결을 만듭니다.
- **터미널 창 열기**: Azure Data Studio에서 터미널(기존 또는 신규)을 엽니다.
- **컨테이너 중지**: 사용자가 실행하면 컨테이너를 중지하는 명령을 터미널에 복사합니다.
- **컨테이너 제거**: 사용자가 실행하면 컨테이너를 제거하는 명령을 터미널에 복사합니다.

## <a name="remote-container-instance"></a>원격 컨테이너 인스턴스

컨테이너 정보 및 대상/호스트 머신 정보를 지정하여 Docker가 설치된 원격 호스트의 Docker 컨테이너에 Azure SQL Edge를 배포할 수 있습니다.  배포를 완료한 후 Notebook 맨 아래에서 연결 링크를 사용할 수 있습니다.  원격 컨테이너 호스트 환경 때문에 컨테이너를 중지하거나 제거하려면 원격 셸에서 실행되도록 명령을 복사해야 합니다.

## <a name="new-azure-iot-hub-and-vm"></a>새 Azure IoT 허브 및 VM

Azure SQL Edge 배포 마법사는 Azure IoT 허브에 연결된 Edge 사용 VM(가상 머신)을 배포하는 데 필요한 몇 가지 Azure 리소스를 만들 수 있습니다. 활성 Azure 구독이 필요합니다. 이 배포는 다음 항목을 만듭니다.

- 리소스 그룹(현재 리소스 그룹을 선택하지 않은 경우)
- 네트워크 보안 그룹
- 가상 머신
- 고정 공용 IP 주소

필요에 따라 프로세스의 일부로 폴더의 dacpac 파일을 압축하여 새 Azure SQL Edge 인스턴스에 배포할 수 있습니다.  dacpac 파일을 제공하면 동일한 리소스 그룹에 Azure Blob Storage 계정이 생성됩니다.

## <a name="existing-device-of-an-azure-iot-hub"></a>Azure IoT 허브의 기존 디바이스

기존 IoT 허브 및 연결된 디바이스가 있는 경우 리소스 그룹, IoT 허브 이름, 디바이스 ID에 따라 Azure SQL Edge를 디바이스에 배포할 수 있습니다.
배포 마법사에서 입력된 IP 주소를 활용하여 Notebook 맨 아래에 빠른 연결 링크가 생성됩니다.

필요에 따라 프로세스의 일부로 폴더의 dacpac 파일을 압축하여 새 Azure SQL Edge 인스턴스에 배포할 수 있습니다.  dacpac 파일을 제공하면 동일한 리소스 그룹에 Azure Blob Storage 계정이 생성됩니다.

## <a name="multiple-devices-of-an-azure-iot-hub"></a>Azure IoT 허브의 여러 디바이스

기존 IoT 허브 및 연결된 디바이스가 있는 경우 리소스 그룹, IoT 허브 이름, 디바이스 선택 [대상 조건](https://docs.microsoft.com/azure/iot-edge/module-deployment-monitoring#target-condition)에 따라 Azure SQL Edge를 디바이스에 배포할 수 있습니다.
배포 마법사에서 입력된 IP 주소를 활용하여 Notebook 맨 아래에 빠른 연결 링크가 생성됩니다.

필요에 따라 프로세스의 일부로 폴더의 dacpac 파일을 압축하여 새 Azure SQL Edge 인스턴스에 배포할 수 있습니다.  dacpac 파일을 제공하면 동일한 리소스 그룹에 Azure Blob Storage 계정이 생성됩니다.

## <a name="next-steps"></a>다음 단계

- [Azure SQL Edge에 대한 자세한 정보](https://docs.microsoft.com/azure/azure-sql-edge/)