---
title: '1단원: Windows Azure 저장소 계정 및 컨테이너 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: efdbd930-cde5-41b0-90ad-58a6cc68dddc
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8a1f8cef9f29c856ab0bc02480221e583a0078f3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62676187"
---
# <a name="lesson-1-create-windows-azure-storage-account-and-container"></a>1단원: Microsoft Azure Storage 계정 및 컨테이너 만들기
  Windows Azure 스토리지에 SQL Server 데이터 파일을 저장하려면 먼저 Windows Azure 스토리지 계정, BLOB 컨테이너 및 공유 액세스 서명을 만들어야 합니다. 1단원에서는 Windows Azure 관리 포털에 로그인하여 스토리지 계정, BLOB 컨테이너 및 공유 액세스 서명을 만드는 과정을 단계별로 안내합니다.  
  
 기본적으로 스토리지 계정의 소유자만 해당 계정 내에서 BLOB, 테이블 및 큐에 액세스할 수 있습니다. 스토리지 계정 액세스 키를 공유하지 않고 이 새로운 향상된 SQL Server 기능을 사용하여 이러한 리소스에 액세스할 수 있으려면 다음을 수행해야 합니다.  
  
-   컨테이너의 사용 권한을 개인으로 설정합니다.  
  
-   공유 액세스 서명을 만듭니다. 이 서명을 사용하면 리소스를 사용할 수 있는 간격과 클라이언트에 부여할 사용 권한을 지정하여 컨테이너, BLOB, 테이블 또는 큐 리소스에 대한 제한된 액세스를 위임할 수 있습니다.  
  
-   저장된 액세스 정책을 사용하여 컨테이너 또는 해당 BLOB에 대한 공유 액세스 서명을 관리합니다. 저장된 액세스 정책을 통해 공유 액세스 서명을 추가로 제어할 수 있을 뿐만 아니라 간단하게 취소할 수도 있습니다.  
  
 자세한 내용은 [Windows Azure 스토리지 리소스에 대한 액세스 관리](https://msdn.microsoft.com/library/windowsazure/ee393343.aspx)를 참조하십시오.  
  
## <a name="create-storage-account"></a>스토리지 계정 만들기  
 Windows Azure 관리 포털에서 스토리지 계정을 만들려면 다음 단계를 수행합니다.  
  
1.  귀하의 계정을 사용하여 [Windows Azure 관리 포털](https://manage.windowsazure.com) 에 로그인합니다. Windows Azure 계정이 없는 경우 [Windows Azure 무료 평가판](http://www.windowsazure.com/pricing/free-trial/)을 사용하십시오.  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-1.gif "SQL 14 CTP2")  
  
2.  단계별 지침을 사용하여 [스토리지 계정을 만듭니다](http://azure.microsoft.com/documentation/articles/storage-create-storage-account/). Windows Azure의 SQL Server 데이터 파일 기능에 사용할 스토리지 계정을 만들 때는 지리적 복제를 선택 취소하거나 해제해야 합니다. 이는 지리적 복제에 참여하는 여러 BLOB에 대해 쓰기 순서가 보장되지 않기 때문입니다. 스토리지 계정이 지리적으로 복제되고 복구가 필요한 경우 손상이 발생합니다.  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-2.gif "SQL 14 CTP2")  
  
## <a name="create-a-blob-container"></a>BLOB 컨테이너 만들기  
 Windows Azure에서 컨테이너는 그룹화된 BLOB 집합을 제공합니다. 모든 blob는 컨테이너에 있어야 합니다. 스토리지 계정은 개수에 제한 없이 컨테이너를 포함할 수 있지만 적어도 하나는 포함해야 합니다. 컨테이너에는 개수에 제한 없이 blob를 저장할 수 있습니다. 스토리지 크기 제한에 대한 최신 정보는 [.NET에서 Windows Azure BLOB 스토리지 서비스를 사용하는 방법](http://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)을 참조하십시오.  
  
 Windows Azure에서 컨테이너를 만들려면 다음 단계를 수행합니다.  
  
1.  [Windows Azure 관리 포털](https://manage.windowsazure.com)에 로그인합니다.  
  
2.  스토리지 계정을 선택하고 **컨테이너** 탭을 클릭한 다음 화면 맨 아래에서 **컨테이너 추가** 를 클릭하면 새 대화 상자가 열립니다.  
  
3.  컨테이너 이름을 입력합니다.  
  
4.  **액세스 형식** 에서 **개인**을 선택합니다. 액세스 형식을 개인으로 설정하면 Windows Azure 계정 소유자만 컨테이너 및 BLOB 데이터를 읽을 수 있습니다.  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-4.gif "SQL 14 CTP2")  
  
> [!NOTE]  
>  프로그래밍 방식으로 컨테이너를 만들려면 REST API를 사용할 수도 있습니다. 자세한 내용은 [컨테이너 만들기](https://msdn.microsoft.com/library/windowsazure/dd179468.aspx) 및 [Windows Azure 스토리지 서비스 REST API 참조](https://msdn.microsoft.com/library/windowsazure/dd179355.aspx)를 참조하세요.  
  
 **다음 단원:**  
  
 [2단원. 컨테이너에 정책을 만들고 공유 액세스 서명 생성 &#40;SAS&#41; 키](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)  
  
  
