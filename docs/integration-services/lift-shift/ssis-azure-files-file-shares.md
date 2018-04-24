---
title: 온-프레미스 및 Azure에서 파일 공유의 파일 저장 및 검색 | Microsoft Docs
description: 이 문서에서는 SSIS로 온-프레미스와 Azure에서 파일 시스템 및 파일 공유를 사용하는 방법을 설명합니다
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b9fb260101c1f814c85360d3fe5998b6e9234101
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="store-and-retrieve-files-on-file-shares-on-premises-and-in-azure-with-ssis"></a>SSIS로 온-프레미스 및 Azure에서 파일 공유의 파일 저장 및 검색
이 문서에서는 Azure에서 로컬 파일 시스템을 SSIS로 사용하는 패키지를 리프트 앤 시프트할 때 SSIS(SQL Server Integration Services) 패키지를 업데이트하는 방법을 설명합니다.

> [!IMPORTANT]
> 현재, SSISDB(SSIS 카탈로그 데이터베이스)는 단일 집합의 액세스 자격 증명만을 지원합니다. 따라서 Azure SSIS IR(Integration Runtime)은 여러 자격 증명을 사용하여 여러 온-프레미스 파일 공유 및 Azure Files 공유에 연결할 수 없습니다.

## <a name="store-temporary-files"></a>임시 파일 저장
단일 패키지를 실행하는 동안 임시 파일을 저장하고 처리해야 하는 경우 패키지는 Azure SSIS Integration Runtime 노드의 현재 작업 디렉터리(`.`) 또는 임시 폴더(`%TEMP%`)를 사용할 수 있습니다.

## <a name="store-files-across-multiple-package-executions"></a>여러 패키지 실행 간 파일 저장
영구 파일을 저장하고 처리하고 여러 패키지 실행 간에 유지해야 하는 경우 온-프레미스 파일 공유 또는 Azure Files를 사용할 수 있습니다.

### <a name="use-on-premises-file-shares"></a>온-프레미스 파일 공유 사용
**온-프레미스 파일 공유**를 계속해서 사용하려면 Azure에서 로컬 파일 시스템을 SSIS로 사용하는 패키지를 리프트 앤 시프트할 때 다음 작업을 수행합니다.
1.  로컬 파일 시스템에서 온-프레미스 파일 공유로 파일을 전송합니다.
2.  온-프레미스 파일 공유를 VNet(Azure 가상 네트워크)에 조인합니다.
3.  Azure SSIS IR을 동일한 VNet에 조인합니다. 자세한 내용은 [Azure SSIS 통합 런타임을 가상 네트워크에 조인](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network)을 참조하세요.
4.  Windows 인증을 사용하는 액세스 자격 증명을 설정하여 Azure SSIS IR을 동일한 VNet 내의 온-프레미스 파일 공유에 연결합니다. 자세한 내용은 [Windows 인증으로 온-프레미스 데이터 원본 및 Azure 파일 공유에 연결](ssis-azure-connect-with-windows-auth.md)을 참조하세요.
5.  패키지의 로컬 파일 경로를 온-프레미스 파일 공유를 가리키는 UNC 경로로 업데이트합니다. 예를 들어 `C:\abc.txt`를 `\\<on-prem-server-name>\<share-name>\abc.txt`로 업데이트합니다.

### <a name="use-azure-file-shares"></a>Azure 파일 공유 사용
**Azure Files**를 사용하려면 Azure에서 로컬 파일 시스템을 SSIS로 사용하는 패키지를 리프트 앤 시프트할 때 다음 작업을 수행합니다.
1.  로컬 파일 시스템에서 Azure Files로 파일을 전송합니다. 자세한 내용은 [Azure Files](https://azure.microsoft.com/services/storage/files/)를 참조하세요.
2.  Windows 인증을 사용하는 액세스 자격 증명을 설정하여 Azure SSIS IR을 Azure Files에 연결합니다. 자세한 내용은 [Windows 인증으로 온-프레미스 데이터 원본 및 Azure 파일 공유에 연결](ssis-azure-connect-with-windows-auth.md)을 참조하세요.
3.  패키지의 로컬 파일 경로를 Azure Files를 가리키는 UNC 경로로 업데이트합니다. 예를 들어 `C:\abc.txt`를 `\\<storage-account-name>.file.core.windows.net\<share-name>\abc.txt`로 업데이트합니다.
