---
title: 어플라이언스 네트워크 구성-Analytics Platform System | Microsoft Docs
description: Analytics Platform System (APS) 어플라이언스 빌드되어 모든 서버 및 IHV의 공장 현장에서 적용 가능한 장치 전체에서 IP 주소 수정 집합으로 구성 됩니다. 어플라이언스의 배달 시 특정 고객의 데이터 센터 요구 사항에 맞게 (이더넷) 외부 IP 주소로 다시 구성 해야 합니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d11184c1fd12ae40188ef4e4442e7f9b7fb6b04a
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909813"
---
# <a name="appliance-network-configuration-for-analytics-platform-system"></a>Analytics Platform System에 대 한 어플라이언스 네트워크 구성
Analytics Platform System (APS) 어플라이언스 빌드되어 모든 서버 및 IHV의 공장 현장에서 적용 가능한 장치 전체에서 IP 주소 수정 집합으로 구성 됩니다. 어플라이언스의 배달 시 특정 고객의 데이터 센터 요구 사항에 맞게 (이더넷) 외부 IP 주소로 다시 구성 해야 합니다.  
  
> [!NOTE]  
> PDW V1 필요한 8 IP 외부 (*고객 연결*) 노드를 랙 각 컨트롤에 대 한 외부 연결을 제공 하는 주소입니다. PDW 2012 (V2) IP 주소를 통해 외부적으로 어플라이언스의 모든 구성 요소가 노출 하 여 네트워크 통신을 향상 합니다. 이 방법은 더욱 강력한 디자인 비용을 절감 및 유연성을 향상 하 고 데이터 이동, 데이터 로드 및 Hadoop 통합 향상을 제공 합니다. 필요한 IP 주소 수가 어플라이언스의 노드 수에 따라 달라 집니다. 이 더 큰 블록의 IP 주소를 수용할 수 있도록 고객 PDW에 대 한 별도 서브넷을 설정 해야 합니다. 이 서브넷 내에 충분 한 IP 주소 공간 (최대 250 개의 주소) 최대 5 개의 PDW 랙의 구성 요소에 맞게 있을 것입니다.  
  
합니다 **네트워크 구성** 페이지 분석 플랫폼 시스템 어플라이언스 노드에 대 한 외부 연결 네트워크 설정을 볼 수 있습니다. 이 페이지는 읽기 전용입니다.  
  
![DWConfig 어플라이언스 네트워크](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>어플라이언스 네트워크 구성을 업데이트 하려면  
편집 하 여 패브릭 도메인 및 작업 도메인의 IP 주소를 변경 합니다 **AplianceInfo.xml** 파일과 다음 설치 프로그램을 실행 합니다. 이 작업은 오프 라인 작업입니다. PDW 영역 IP 주소가 변경 될 때 자동으로 중지 됩니다.  
  
> [!NOTE]  
> 도메인 이름 설정 중에 제공 및 6 영숫자 문자, 문자로 시작까지으로 지정 됩니다. F, P. 부터는 PDW 작업 도메인부터 fabric 도메인을 생성 하는 자주 명명 시스템 이 형식의 도움말 파일 항목 전체에서 간주 됩니다 있지만 필요 하지 않습니다. <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>Analytics Platform System의 IP 주소를 변경 하려면  
  
1.  사용 하 여는 **원격 데스크톱** 응용 프로그램에 연결 **HST01** 작업 도메인 관리자 계정을 사용 합니다.  
  
2.  HST01 노드에서 어플라이언스 정보 파일을 엽니다 **c:\pdwinst\media\AplianceInfo.xml**합니다.  
  
    > [!NOTE]  
    > 파일이 없으면 새 파일을 만들 수 해야 합니다.  
  
3.  필요에 따라 이더넷 IP 값을 업데이트 하 고 파일을 저장 합니다.  
  
4.  명령 프롬프트 창에서 P/F/H 도메인 이름 및 관리자 암호를 사용 하 여 PDW 영역에 대 한 IP 주소를 업데이트 하려면 다음 설치 명령을 실행 합니다.  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>제조업체 참조  
Dell 어플라이언스에 대 한 추가 정보를 참조 하세요.  
  
-   PowerConnect 스위치 지침 [Dell PowerConnect 6200 시리즈 시스템 CLI 참조 가이드](http://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   iDRAC/BMC [통합 Dell 원격 컨트롤러 7 액세스 (iDRAC7) 버전 1.30.30 사용자 가이드](http://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   PDU의 **Dell 랙 PDU 요금제**`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>관련 항목  
[Configuration Manager 시작 &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
