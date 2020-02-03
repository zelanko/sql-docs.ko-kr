---
title: Microsoft Azure Storage에 연결
ms.custom: seo-lt-2019
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.windowsazurestorage.connect.f1
- SQL13.SWB.WINDOWSAZURESTORAGE.CONNECT.F1
ms.assetid: ''
author: markingmyname
ms.author: maghan
ms.openlocfilehash: eb943430136a1406ea18b9c387c98fbec6fd27cf
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75245020"
---
# <a name="connect-to-microsoft-azure-storage"></a>Microsoft Azure Storage에 연결
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
**Azure Storage 연결** 대화 상자를 사용하여 스토리지 계정을 지정하고 Azure 연결의 유효성을 검사할 수 있습니다.  
  
## <a name="options"></a>옵션  
Azure 계정에 대해 다음 정보를 지정한 후 **다음**을 클릭하여 계속합니다.  
  
1.  **스토리지 계정** - 스토리지 계정 이름을 지정합니다.

   >[!NOTE]
   > [범용 스토리지 계정](https://docs.microsoft.com/azure/storage/storage-introduction#azure-storage-services)에만 연결할 수 있습니다. 다른 유형의 스토리지 계정에 연결하면 다음과 유사한 오류 메시지가 발생할 수 있습니다.
   >
   >  HTTP 헤더 중 하나에 대한 값 형식이 올바르지 않습니다. (Microsoft.SqlServer.StorageClient).
   >
   >  원격 서버에서 오류를 반환했습니다. (400) 잘못된 요청. (System)

2.  **계정 키** - 지정한 스토리지 계정의 계정 키를 지정합니다.  
  
3.  **보안 엔드포인트 사용(HTTPS)** – 이 옵션은 암호화된 통신 및 네트워크 웹 서버의 보안 ID를 사용합니다.  
  
4.  **계정 키 저장** - 이 옵션은 암호화된 파일에 암호를 저장합니다.  
  
