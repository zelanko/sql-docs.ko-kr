---
title: 구독 설정 및 파일 공유 계정(구성 관리자) | Microsoft Docs
ms.date: 05/31/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.suite: pro-bi
ms.topic: conceptual
f1_keywords:
- SQL13.rsconfigtool.subscriptionsettings.F1
ms.assetid: fefa7bdb-b5f2-4db7-b91c-b58869279f3c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5b43410d160261cc3b60d675829fd519d11e9ec7
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43280491"
---
# <a name="subscription-settings-and-a-file-share-account-configuration-manager"></a>구독 설정 및 파일 공유 계정(구성 관리자)
  **구성 관리자의** 구독 설정 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 페이지를 사용하면 기본 모드 보고서 서버 및 파일 공유 구독에 대한 파일 공유 계정을 구성할 수 있습니다. 파일 공유 계정을 사용하면 보고서를 파일 공유로 전달하는 여러 구독에서 단일 자격 증명 집합을 사용할 수 있습니다. 자격 증명을 변경해야 하는 경우 파일 공유 계정에 대한 구성을 변경하면 각각의 개별 구독을 업데이트할 필요가 없습니다.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 파일 공유 구독에서 사용할 수 있는 두 가지 워크플로:  
  
-   신규 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 릴리스에서 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 관리자는 일대다 구독에서 사용할 수 있는 단일 파일 공유 계정을 구성할 수 있습니다. **파일 공유 계정 지정**을 구성한 후 개별 구독 구성 페이지에서 **파일 공유 계정 사용**을 선택합니다.  
  
-   개별 구독을 대상 파일 공유에 대한 특정 자격 증명으로 구성합니다.  
  
-   또한, 두 가지 방법을 혼용하여 일부 파일 공유 구독은 중앙식 파일 공유 계정을 사용하고 다른 구독은 특정 자격 증명을 사용하도록 할 수 있습니다.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 기본 모드입니다.  
  
## <a name="specify-a-file-share-account"></a>파일 공유 계정 지정  
 이 옵션을 선택하면 보고서 서버에서 파일 공유에 액세스하는 데 사용할 계정을 제공할 수 있습니다. 파일 공유 계정을 구성하는 경우 모든 사용자는 보고서를 파일 공유로 전송하도록 구성된 모든 구독에서 계정을 선택할 수 있습니다. 이 옵션을 선택하지 않으면 파일 공유 계정을 모든 구독에서 사용할 수 **없습니다** .  
  
 파일 공유 계정으로 구성한 계정이 모든 파일 공유에 대하여 읽기 및 쓰기 권한이 있어 사용자가 파일 공유 전송을 사용할 수 있는지 확인해야 합니다.  
  
 다음 그림은 파일 공유 전송을 위해 구성된 구독에서 사용자에게 표시되는 사항을 보여줍니다. 파일 공유 계정이 구성되지 않은 경우 **파일 공유 계정 사용** 이 비활성화됩니다.  
  
 ![구성 관리자 파일 공유 계정](../../reporting-services/install-windows/media/ssrs-fileshare-account.png "구성 관리자 파일 공유 계정")  
  
## <a name="prevent-privilege-escalation-or-elevated-privileges"></a>권한 상승 또는 상승된 권한 방지  
  
> [!IMPORTANT]
> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 계정은 구독 배달을 제어하고 파일 공유 구독에서 사용되는 계정과 상호작용합니다. Windows 보안 기능은 1) [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 계정 및 2) 파일 공유 계정에서 사용된 계정을 조합하여 사용할 수 없습니다. 예를 들어 기본 운영 체제 계정이 파일 공유 계정에서 사용된 경우 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스 계정은 가장 권한이 있는 다른 서비스 계정이어야 합니다. 명시적 파일 공유 계정 및 암호가 구성된 경우 파일 공유 계정은 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 서비스를 실행하는 컴퓨터에 로그온할 수 있는 권한이 있어야 합니다. 파일 공유 계정에 필수 권한이 없는 경우 파일 공유 계정을 사용하는 구독은 다음과 유사한 오류가 발생하여 실패합니다.  
>   
>  `“Failure writing file {file} : An impersonation error occurred using the security context of the current user.”`  
  
## <a name="powershell-sample-to-audit-use-of-the-file-share-account"></a>파일 공유 계정 사용을 감사하기 위한 PowerShell 샘플  
 다음 Windows PowerShell 스크립트를 실행하면 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 파일 공유 계정 **을 사용하도록 구성된 모든**구독이 나열됩니다. `SERVERNAME` 을(를) 보고서 서버에 대한 적절한 값으로 업데이트합니다.  
  
```  
# get all file share subscriptions using the default file share account  
$extensionNameMatch = "Report Server FileShare"  
$extensionSettingMatch = "DEFAULTCREDENTIALS"  
$valueMatch = "True"  
  
# filter for subscriptions that have a given extension setting  
filter script:extensionSettingFilter  
{  
    # subscription must match the extension name  
    if($_.DeliverySettings.Extension -eq $extensionNameMatch)  
    {  
        # locate the extension parameter of interest  
        ForEach($extensionParameter in $_.DeliverySettings.ParameterValues)  
        {  
            # if the setting has the desired value, return the subscription  
            if($extensionParameter.Name -eq $extensionSettingMatch -and $extensionParameter.Value -eq $valueMatch)  
            {  
                $_  
                break  
            }  
        }  
    }  
}  
  
$rs2010 = New-WebServiceProxy -Uri "http:// SERVERNAME/ReportServer/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
$subscriptions = $rs2010.ListSubscriptions("/");  
  
Write-Host "----- File share subscriptions using the default file share account ----";  
Write-Host "-------------------------------------------------------------------------- ";  
$subscriptions | extensionSettingFilter | select report, owner, status, lastexecuted, description, subscriptionid | format-table -auto  
  
```  
  
 스크립트의 출력은 다음과 유사합니다.  
  
 `----- File share subscriptions using the default file share account ----`  
  
 `-----------------------------------------------------------------------------------------------------`  
  
 `Report                    Owner          Status   LastExecuted         SubscriptionID`  
  
 `------------------------  -------------- -------- -------------------- ------------------------------------`  
  
 `Aworks_sales_by_territory DOMAIN\UserName Disabled 10/5/2014 1:04:04 PM e843bc2b-023e-45a3-ba23-22f9dc9a0934`  
  
## <a name="see-also"></a>참고 항목  
 [Reporting Services의 파일 공유 배달](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)   
 [기본 모드 보고서 서버 구독 만들기 및 관리](../../reporting-services/subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)
  
  
