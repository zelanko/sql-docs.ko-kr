---
title: Azure Arc 확장(미리 보기)
description: Azure Arc 확장을 설치하고 사용하여 Azure Arc 데이터 서비스를 체험하는 방법을 알아봅니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: a541b994b33355fb5df8ebf856681d588e82cc2d
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91111737"
---
# <a name="azure-arc-extension-for-azure-data-studio-preview"></a>Azure Data Studio용 Azure Arc 확장(미리 보기)

[Azure Arc 확장(미리 보기)](https://aka.ms/azurearcdata-docs)은 Azure Arc 데이터 서비스 리소스를 만들고 관리하기 위한 확장입니다.

**주요 작업은 다음과 같습니다.**
- 리소스 만들기
    - 데이터 컨트롤러
    - Azure Arc용 SQL Managed Instance
    - Azure Arc용 PostgreSQL
- 리소스 관리
    - 데이터 컨트롤러 보기 대시보드
    - Azure Arc용 SQL Managed Instance 보기 대시보드
    - Azure Arc용 PostgreSQL 보기 대시보드
- Azure Arc Jupyter Book 실행

## <a name="install-the-extension"></a>확장 설치
- 갤러리에서 **Azure Data CLI** 확장을 설치합니다.
- 갤러리에서 **Azure Arc** 확장을 설치합니다.
- Azure Data Studio 다시 시작

## <a name="sign-in-with-azure-account"></a>Azure 계정으로 로그인
1. 왼쪽 아래에서 계정 선택
1. 계정 추가 선택
1. 이 작업을 수행하면 브라우저가 시작됩니다. Azure 계정에 로그인합니다.

## <a name="create-a-resource"></a>리소스 만들기
이 확장은 Azure Arc 데이터 컨트롤러, Azure Arc용 Postgres, Azure Arc용 SQL Managed Instance의 배포를 지원합니다. 배포는 기본 제공 배포 마법사를 통해 수행할 수 있습니다.

1. 왼쪽 작업 막대에서 연결 뷰렛 선택
1. 세 개의 점을 선택하고 **새 배포**를 선택합니다.
1. 프롬프트에 따라 새 Azure Arc 리소스를 만듭니다.

## <a name="manage-a-resource"></a>리소스 관리
azdata, Azure Portal 또는 Azure Data Studio에서 Azure Arc 데이터 컨트롤러를 배포한 후 Azure Data Studio에서 데이터 컨트롤러에 연결할 수 있습니다.

1. 왼쪽 작업 막대에서 연결 뷰렛을 엽니다.
1. **Azure Arc 컨트롤러** 확장
1. **연결 컨트롤러** 선택
1. 매개 변수를 입력한 후 연결합니다.

연결되면 데이터 컨트롤러에 배포된 리소스를 볼 수 있습니다. 그런 다음, 마우스 오른쪽 단추를 클릭하고 **관리**를 선택하여 리소스 대시보드에 액세스할 수 있습니다.  

대시보드는 Azure Portal에서 열 수 있는 옵션을 포함하여 리소스에 대한 추가 정보를 제공합니다.

## <a name="next-steps"></a>다음 단계
Azure Arc 데이터 서비스에 대해 자세히 알아보려면 [설명서를 확인](https://aka.ms/azurearcdata-docs)하세요.
