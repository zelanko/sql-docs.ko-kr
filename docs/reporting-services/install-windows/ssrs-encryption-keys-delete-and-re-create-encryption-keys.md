---
title: "삭제 하 고 암호화 키 (SSRS 구성 관리자)를 다시 만드는 | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- re-creating encryption keys
- encryption keys [Reporting Services]
- deleting encryption keys
- symmetric keys [Reporting Services]
- removing encryption keys
- resetting encryption keys
ms.assetid: 201afe5f-acc9-4a37-b5ec-121dc7df2a61
caps.latest.revision: 9
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b042bef86620c773f39f81ea16a62b3d9c4c2a6a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/09/2017

---
# <a name="ssrs-encryption-keys---delete-and-re-create-encryption-keys"></a>SSRS 암호화 키-삭제 및 다시 암호화 키를 만들기
  암호화 키를 삭제했다가 다시 만드는 작업은 정기적인 암호화 키 유지 관리 작업에 해당되지 않습니다. 보고서 서버가 위협을 받을 때나 보고서 서버 데이터베이스에 더 이상 액세스할 수 없을 때 마지막 수단으로 이러한 태스크를 수행합니다.  
  
-   기존 대칭 키가 노출된 것으로 판단되면 대칭 키를 다시 만듭니다. 또한 보안을 향상시키기 위해 정기적으로 키를 다시 만들 수 있습니다.  
  
-   대칭 키를 복원할 수 없는 경우 기존 암호화 키를 삭제하고 암호화된 내용을 비활성화합니다.  
  
## <a name="re-creating-encryption-keys"></a>암호화 키 다시 만들기  
 허가되지 않은 사용자가 대칭 키를 알고 있다고 간주되거나 보고서 서버가 공격을 받고 있어 예방 차원에서 대칭 키를 다시 설정하려는 경우 대칭 키를 다시 만들 수 있습니다. 대칭 키를 다시 만들면 암호화된 모든 값이 새 값을 사용하여 다시 암호화됩니다. 확장 배포에서 여러 보고서 서버를 실행할 경우 대칭 키의 모든 복사본이 새 값으로 업데이트됩니다. 보고서 서버는 사용 가능한 공개 키를 사용하여 배포의 각 서버에 대해 해당 대칭 키를 업데이트합니다.  
  
 보고서 서버가 작동 상태일 때만 대칭 키를 다시 만들 수 있습니다. 암호화 키를 다시 만들고 내용을 다시 암호화하면 서버 작동이 중단됩니다. 다시 암호화하는 동안 서버를 오프라인으로 만들어야 합니다. 다시 암호화하는 동안에는 보고서 서버에 대해 요청이 수행되면 안 됩니다.  
  
 Reporting Services 구성 도구나 **rskeymgmt** 유틸리티를 사용하여 대칭 키와 암호화된 데이터를 다시 설정할 수 있습니다. 대칭 키를 만드는 방법은 [보고서 서버 초기화&#40;SSRS 구성 관리자&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)를 참조하세요.  
  
### <a name="how-to-re-create-encryption-keys-reporting-services-configuration-tool"></a>암호화 키를 다시 만드는 방법(Reporting Services 구성 도구)  
  
1.  rsreportserver.config 파일에서 **IsWebServiceEnabled** 속성을 수정하여 보고서 서버 웹 서비스 및 HTTP 액세스를 사용하지 않도록 설정합니다. 이 단계에서는 서버를 완전히 종료하지 않고 보고서 서버로 보내는 인증 요청을 임시로 중지합니다. 키를 다시 만들 수 있는 최소한의 서비스가 필요합니다.  
  
     보고서 서버 확장 배포를 위해 암호화 키를 다시 만들 경우 배포의 모든 인스턴스에서 이 속성을 사용하지 않도록 설정합니다.  
  
    1.  Windows 탐색기를 열고 *drive*:\Program Files\Microsoft SQL Server\\*report_server_instance*\Reporting Services로 이동합니다. 여기서 *drive* 는 드라이브 문자이고 *report_server_instance* 는 웹 서비스 및 HTTP 액세스를 사용하지 않도록 설정할 보고서 서버 인스턴스에 해당하는 폴더 이름입니다. 예를 들면 C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services와 같습니다.  
  
    2.  rsreportserver.config 파일을 엽니다.  
  
    3.  **IsWebServiceEnabled** 속성에 **False**를 지정한 다음 변경 내용을 저장합니다.  
  
2.  Reporting Services 구성 도구를 시작한 후 구성하려는 보고서 서버 인스턴스에 연결합니다.  
  
3.  암호화 키 페이지에서 **변경**을 클릭합니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  보고서 서버 Windows 서비스를 다시 시작합니다. 확장 배포를 위해 암호화 키를 다시 만들 경우 모든 인스턴스에서 해당 서비스를 다시 시작합니다.  
  
5.  rsreportserver.config 파일에서 **IsWebServiceEnabled** 속성을 수정하여 웹 서비스 및 HTTP 액세스를 다시 사용하도록 설정합니다. 확장 배포 구성에서 작업할 경우에는 모든 인스턴스에 대해 이 작업을 수행합니다.  
  
### <a name="how-to-re-create-encryption-keys-rskeymgmt"></a>암호화 키를 다시 만드는 방법(rskeymgmt)  
  
1.  보고서 서버 웹 서비스 및 HTTP 액세스를 사용하지 않도록 설정합니다. 이전 절차의 지시대로 웹 서비스 작업을 중지합니다.  
  
2.  보고서 서버를 호스팅하는 컴퓨터에서 **rskeymgmt.exe** 를 로컬로 실행합니다. **-s** 인수를 사용하여 대칭 키를 다시 설정합니다. 다른 인수는 필요하지 않습니다.  
  
    ```  
    rskeymgmt -s  
    ```  
  
3.  Reporting Services Windows 서비스를 다시 시작합니다.  
  
## <a name="deleting-unusable-encrypted-content"></a>사용할 수 없는 암호화된 내용 삭제  
 여타의 이유로 암호화 키를 복원할 수 없는 경우 보고서 서버는 암호를 해독할 수 없으며 해당 키로 암호화된 어떠한 데이터도 사용할 수 없게 됩니다. 보고서 서버를 작동 상태로 되돌리려면 보고서 서버 데이터베이스에 현재 저장되어 있는 암호화된 값을 삭제한 후 필요한 값을 수동으로 다시 지정해야 합니다.  
  
 암호화 키를 삭제하면 보고서 서버 데이터베이스에서 모든 대칭 키 정보가 제거되고 암호화된 모든 내용이 삭제됩니다. 암호화되지 않은 데이터는 모두 그대로 남아 있으며 암호화된 내용만 제거됩니다. 암호화 키를 삭제하면 보고서 서버는 새 대칭 키를 추가하여 자체적으로 다시 초기화됩니다. 암호화된 내용을 삭제하면 다음 상황이 발생합니다.  
  
-   공유 데이터 원본의 연결 문자열이 삭제됩니다. 보고서를 실행하면 "ConnectionString 속성이 초기화되지 않았습니다"라는 오류가 발생합니다.  
  
-   저장된 자격 증명이 삭제됩니다. 프롬프트된 자격 증명을 사용하도록 보고서 및 공유 데이터 원본이 다시 구성됩니다.  
  
-   모델을 기반으로 하며 저장된 자격 증명을 사용하여 구성되거나 자격 증명 없이 구성된 공유 데이터 원본을 요구하는 보고서는 실행되지 않습니다.  
  
-   구독이 비활성화됩니다.  
  
 암호화된 내용을 삭제한 경우 다시 복구할 수 없습니다. 연결 문자열과 저장된 자격 증명을 다시 지정하고 구독을 활성화해야 합니다.  
  
 Reporting Services 구성 도구나 **rskeymgmt** 유틸리티를 사용하여 값을 제거할 수 있습니다.  
  
### <a name="how-to-delete-encryption-keys-reporting-services-configuration-tool"></a>암호화 키를 삭제하는 방법(Reporting Services 구성 도구)  
  
1.  Reporting Services 구성 도구를 시작한 후 구성하려는 보고서 서버 인스턴스에 연결합니다.  
  
2.  **암호화 키**를 클릭한 후 **삭제**를 클릭합니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  보고서 서버 Windows 서비스를 다시 시작합니다. 확장 배포의 경우 모든 보고서 서버 인스턴스에 대해 이 작업을 수행합니다.  
  
### <a name="how-to-delete-encryption-keys-rskeymmgt"></a>암호화 키를 삭제하는 방법(rskeymmgt)  
  
1.  보고서 서버를 호스팅하는 컴퓨터에서 **rskeymgmt.exe** 를 로컬로 실행합니다. **-d** 적용 인수를 사용해야 합니다. 다음은 인수 지정 예입니다.  
  
    ```  
    rskeymgmt -d  
    ```  
  
2.  보고서 서버 Windows 서비스를 다시 시작합니다. 확장 배포의 경우 모든 보고서 서버 인스턴스에 대해 이 작업을 수행합니다.  
  
### <a name="how-to-re-specify-encrypted-values"></a>암호화된 값을 다시 지정하는 방법  
  
1.  각 공유 데이터 원본에 대해 연결 문자열을 다시 입력해야 합니다.  
  
2.  저장된 자격 증명을 사용하는 각 보고서 및 공유 데이터 원본의 경우 사용자 이름과 암호를 다시 입력한 후 저장해야 합니다. 자세한 내용은 [온라인 설명서에서](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) 보고서 데이터 원본에 대한 자격 증명 및 연결 정보 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 참조하세요.  
  
3.  각 데이터 기반 구독에 대해 각 구독을 열고 구독 데이터베이스에 대한 자격 증명을 다시 입력합니다.  
  
4.  암호화된 데이터(파일 공유 배달 확장 프로그램과 암호화를 사용하는 타사의 배달 확장 프로그램 포함)를 사용하는 구독의 경우 각 구독을 열고 자격 증명을 다시 입력합니다. 보고서 서버 전자 메일 배달을 사용하는 구독은 암호화된 데이터를 사용하지 않으므로 키가 달라져도 영향을 받지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [구성 및 암호화 키 &#40; 관리 SSRS 구성 관리자 &#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [저장소 암호화 된 보고서 서버 데이터 &#40; SSRS 구성 관리자 &#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  

