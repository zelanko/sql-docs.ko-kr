---
title: Microsoft Azure 구독에 연결 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: cca5a270-643f-4677-8802-98464f19f82a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 765763ae01183d0907e5371cf1420205cd5737b5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68076129"
---
# <a name="connect-to-a-microsoft-azure-subscription"></a>Microsoft Azure 구독에 연결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
**Microsoft 구독에 연결** 을 사용하여 SQL Server의 인스턴스가 포함된 기존 Azure blob 컨테이너를 등록합니다.  대화 상자를 통해 Azure blob 컨테이너에 저장된 액세스 정책 및 공유 액세스 서명을 만든 다음 SQL Server 자격 증명을 만듭니다.  이 대화 상자는 SQL Server Management Studio의 백업 또는 복원 작업 및 URL 디바이스가 관련된 작업을 사용할 때 표시됩니다.

## <a name="limitation"></a>제한 사항
**Microsoft 구독에 연결** 은 서비스 관리(클래식) 배포 모델을 통해 생성된 Azure Storage 계정에서만 작동합니다.  Azure 배포 모델에 대한 자세한 내용은 [Azure Resource Manager 및 클래식 배포](https://azure.microsoft.com/documentation/articles/resource-manager-deployment-model/)를 참조하세요.

## <a name="options"></a>옵션
**로그인**     
적절한 Azure 계정으로 로그인합니다.

**사용할 구독 선택**      
드롭다운 목록에서 원하는 구독을 선택합니다.

**스토리지 계정 선택**  
드롭다운 목록에서 원하는 스토리지 계정을 선택합니다.

**Blob 컨테이너 선택**   
드롭다운 목록에서 원하는 blob 컨테이너를 선택합니다.

**공유 액세스 정책 만료**   
공유 액세스 정책이 지정된 날짜에 만료됩니다.  기본 만료 날짜는 생성 날짜로부터 1년입니다.  원하는 대로 수정합니다.

**공유 액세스 서명 생성**   
서식 있는 입력란에는 생성된 공유 액세스 서명이 표시됩니다.

**CREATE CREDENTIAL**   
단추는 저장된 액세스 정책 및 공유 액세스 서명을 생성한 다음 SQL Server 자격 증명을 만듭니다.
