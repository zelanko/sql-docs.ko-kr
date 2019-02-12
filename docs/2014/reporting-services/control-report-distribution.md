---
title: 보고서 배포 제어 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], report distribution
- subscriptions [Reporting Services], e-mail
- subscriptions [Reporting Services], file share delivery
- file share delivery [Reporting Services]
- e-mail [Reporting Services]
- subscriptions [Reporting Services], security
- mail [Reporting Services]
ms.assetid: 8f15e2c6-a647-4b05-a519-1743b5d8654c
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e3911bfcd923b26251c81809c9671981e0ff84e9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56018045"
---
# <a name="control-report-distribution"></a>보고서 배포 제어
  전자 메일 및 파일 공유 배포와 관련된 보안 위험을 줄이도록 보고서 서버를 구성할 수 있습니다.  
  
## <a name="securing-reports"></a>보고서 보안  
 보고서 배포 제어의 첫 단계는 무단 액세스로부터 보고서를 보호하는 것입니다. 구독에서 사용하려면 보고서는 개별 배달에 따라 변경되지 않는 저장된 자격 증명 집합을 사용해야 합니다. 보고서 서버의 보고서에 액세스할 수 있는 모든 사용자는 보고서를 실행하고 배포할 수 있습니다. 이를 방지하려면 보고서가 필요한 사용자만 보고서에 액세스할 수 있도록 제한해야 합니다. 자세한 내용은 [보고서 및 리소스 보안](security/secure-reports-and-resources.md) 하 고 [폴더 보안](security/secure-folders.md)합니다.  
  
 데이터베이스 보안을 사용하여 액세스 권한을 부여하는 주요 기밀 보고서는 구독을 통해 배포할 수 없습니다.  
  
> [!IMPORTANT]  
>  보고서는 파일로 전송됩니다. 파일에 적용되는 위험 및 보호 방법이 디스크에 저장되거나 첨부 파일로 전달되는 보고서에 동일하게 적용됩니다. 파일에 액세스할 수 있는 모든 사용자는 파일을 임의로 배포하거나 사용할 수 있습니다.  
  
## <a name="controlling-e-mail-delivery"></a>전자 메일 배달 제어  
 전자 메일 배포를 특정 호스트 도메인으로 제한하도록 보고서 서버를 구성할 수 있습니다. 예를 들어 보고서 서버가 RSReportServer 구성 파일에 나열된 도메인을 제외한 모든 도메인에 보고서를 배달하지 못하도록 할 수 있습니다.  
  
 구독의 **받는 사람** 필드를 숨기도록 구성 설정을 지정할 수도 있습니다. 이런 경우 보고서는 구독을 정의하는 사용자에게만 배달됩니다. 그러나 사용자에게 보고서를 보낸 다음에는 보고서가 전달되지 않도록 명시적으로 방지할 수 없습니다.  
  
 보고서 배포를 제어하는 가장 효율적인 방법은 보고서 서버 URL로만 보내도록 보고서 서버를 구성하는 것입니다. 보고서 서버는 Windows 인증 및 역할 기반 인증 모델을 사용하여 보고서에 대한 액세스를 제어합니다. 보기 권한이 없는 사용자에게 전자 메일을 통해 보고서가 실수로 전달된 경우 보고서 서버는 해당 보고서를 표시하지 않습니다.  
  
## <a name="controlling-file-share-delivery"></a>파일 공유 배달 제어  
 파일 공유 배달은 하드 디스크의 파일로 보고서를 보내는 데 사용됩니다. 파일이 디스크에 저장된 후에는 보고서 서버에서 사용자 액세스를 제어하는 데 사용하는 역할 기반 보안 모델의 적용을 더 이상 받지 않습니다. 디스크로 배달된 보고서를 보호하려면 파일 자체나 파일이 포함된 폴더에 ACL(Access Control 목록)을 배치할 수 있습니다. 운영 체제에 따라 추가 보안 옵션을 사용할 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [전자 메일 배달을 위한 보고서 서버 구성 &#40;SSRS 구성 관리자&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [구독 및 배달&#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [기본 모드 보고서 서버 구독 만들기 및 관리](../../2014/reporting-services/create-manage-subscriptions-native-mode-report-servers.md)  
  
  
