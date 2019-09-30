---
title: Azure Blob Storage에 연결(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e2e482b8-5f90-48c5-93fb-b412ed52659f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 17330bafe2655f0569f0828706d5e29ed2af3812
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71285359"
---
# <a name="connect-to-azure-blob-storage-sql-server-import-and-export-wizard"></a>Azure Blob Storage에 연결(SQL Server 가져오기 및 내보내기 마법사)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


이 항목에서는 SQL Server 가져오기 및 내보내기 마법사의 **데이터 원본 선택** 또는 **대상 선택** 페이지에서 **Azure Blob Storage** 데이터 원본에 연결하는 방법을 보여 줍니다.

> [!NOTE]
> Azure Blob 원본 또는 대상을 사용하려면 SQL Server Integration Services용 Azure 기능 팩을 설치해야 합니다.
> - 기능 팩을 다운로드하려면 [Azure용 Microsoft SQL Server 2016 Integration Services 기능 팩](https://www.microsoft.com/download/details.aspx?id=49492)을 참조하세요.
> 
> - 자세한 내용은 [Integration Services용 Azure 기능 팩&#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)을 참조하세요.

다음 스크린 샷은 Azure Blob Storage에 연결하도록 구성하는 옵션을 보여 줍니다.

![Azure Blob Storage 연결](../../integration-services/import-export-data/media/azure-blob-storage-connection.png)

## <a name="options-to-specify"></a>지정할 옵션

> [!NOTE]
> 이 데이터 공급자에 대한 연결 옵션은 Azure Blob Storage가 원본 또는 대상인지 여부에 관계없이 동일합니다. 즉 마법사의 **데이터 원본 선택** 및 **대상 선택** 페이지 모두에서 동일한 옵션이 표시됩니다.

 **Azure 계정 사용**  
 온라인 계정을 사용할지 여부를 지정합니다.
  
 **스토리지 계정 이름**  
 Azure 스토리지 계정의 이름을 입력합니다.  
  
**계정 키**  
Azure 스토리지 계정의 키를 입력합니다.  
  
 **HTTPS 사용**  
 스토리지 계정에 연결할 때 사용할 프로토콜(HTTP 또는 HTTPS)을 지정합니다.  
  
 **로컬 개발자 계정 사용**  
 로컬 컴퓨터의 스토리지 에뮬레이터를 사용할지 여부를 지정합니다.  
  
 **Blob 컨테이너 이름**  
 지정된 스토리지 계정에서 사용할 수 있는 스토리지 컨테이너 목록에서 컨테이너를 선택합니다.  
  
 **Blob 파일 형식**  
 텍스트 또는 Avro 파일 형식을 선택합니다.  
  
 **열 구분 기호 문자**  
 텍스트 형식을 선택한 경우 열 구분 기호 문자를 입력합니다.  
  
 **첫 행은 열 이름으로**  
 첫 번째 데이터 행에 열 이름을 포함할지 여부를 지정합니다.  

## <a name="see-also"></a>관련 항목:
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

