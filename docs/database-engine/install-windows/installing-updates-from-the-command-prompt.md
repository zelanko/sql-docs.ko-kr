---
title: 명령 프롬프트에서 업데이트 설치 | Microsoft Docs
description: 이 문서에서는 SQL Server 업데이트 설치를 위한 명령 구문을 설명합니다. 조직의 필요에 따라 설치 스크립트를 테스트하고 수정할 수 있습니다.
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: bc98ba2b-aae9-4d01-aa85-d4c36428cb0b
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: f4c99cbcdbb9d61697b36c2ff57f9ec74726060c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463634"
---
# <a name="installing-updates-from-the-command-prompt"></a>명령 프롬프트에서 업데이트 설치

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

조직의 필요에 따라 설치 스크립트를 테스트하고 수정할 수 있습니다. 
 
## <a name="sample-syntax-for-installation"></a>설치 구문 예제 
업데이트 패키지의 이름은 다양하며 언어, 버전 및 프로세서 구성 요소를 포함할 수 있습니다. 명령 프롬프트에서 <package_name>을 해당하는 업데이트 패키지 이름으로 바꾸어 업데이트를 적용합니다. 
 
- 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 모든 공유 구성 요소(예: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 관리 도구) 업데이트: InstanceName 매개 변수 또는 InstanceID 매개 변수를 사용하여 인스턴스를 지정할 수 있습니다. 준비된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스를 업데이트하려면 InstanceID 매개 변수를 지정해야 합니다.

    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance
    ```
    또는 
    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceID=\<Instance ID>. 
    ```

- 설치 프로그램에서 최신 제품 업데이트를 주 제품 설치와 통합하여 주 제품과 해당 업데이트가 동시에 설치되게 할 수 있습니다. 제품 업데이트를 포함하도록 데이터베이스 엔진 인스턴스의 설치를 준비하려면 

    ```
    setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=PrepareImage /UpdateEnabled=True /UpdateSource=\<path where the update is downloaded> /INSTANCEID=\<Instance ID> /FEATURES=SQLEngine. 
    ```

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공유 구성 요소(예: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 관리 도구)만 업데이트: 

    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch 
    ```

- 컴퓨터에 있는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 모든 공유 구성 요소(예: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 관리 도구) 업데이트: 

    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances. 
    ```

- 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 및 모든 공유 구성 요소(예: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 관리 도구)에서 업데이트 제거: 

    ```
    <package_name>.exe /qs /Action=RemovePatch /InstanceName=MyInstance. 
    ```

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공유 구성 요소(예: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 및 관리 도구)에서만 업데이트 제거: 

    ```
    <package_name>.exe /qs /Action=RemovePatch 
    ```

  > [!NOTE] 
  > 업데이트 설치 관리자는 공유 구성 요소를 항상 최상위 수준의 인스턴스 버전 이상으로 유지합니다. 
 
## <a name="supported-parameters"></a>지원되는 매개 변수 
 
> [!IMPORTANT] 
> 가능한 한 런타임에 보안 자격 증명을 지정하십시오. 스크립트 파일에 자격 증명을 저장해야 하는 경우에는 무단으로 액세스하지 못하도록 파일에 보안을 설정하세요. 
 
|스위치|Description| 
|------------|-----------------| 
|**/?**|무인 설치 명령 프롬프트 도움말을 표시합니다.| 
|**/action=Patch 또는 /action=RemovePatch**|설치 동작으로 Patch 또는 RemovePatch를 지정합니다.| 
|**/allinstances**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트를 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 적용하고 인스턴스를 인식하지 않는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공유 구성 요소에도 적용합니다.| 
|**/instancename=InstanceName** _|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트를 InstanceName이라는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 적용하고 인스턴스를 인식하지 않는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공유 구성 요소에도 적용합니다.| 
|_ */InstanceID=Inst1**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inst1 인스턴스에 적용하고 인스턴스를 인식하지 않는 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공유 구성 요소에도 적용합니다.| 
|**/quiet**|무인 모드로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 업데이트 설치 프로그램을 실행합니다.| 
|**/qs**|진행률 UI 대화 상자만 표시합니다.| 
|**/UpdateEnabled**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램이 제품 업데이트를 검색하고 포함하는지 여부를 지정합니다. 유효한 값은 True와 False 또는 1과 0입니다. 기본적으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에는 검색된 업데이트가 포함됩니다.| 
|**/IAcceptSQLServerLicenseTerms**|무인 설치에 /Q 또는 /QS 매개 변수가 지정된 경우에만 필수입니다.| 
 
 \* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 준비 인스턴스에 업데이트를 적용할 때는 이 매개 변수를 지정할 수 없습니다. 대신 /instanceID 매개 변수를 지정해야 합니다. 
 
## <a name="see-also"></a>참고 항목 
 [SQL Server 서비스 설치 개요](./install-sql-server-servicing-updates.md) 
 
