---
title: 영어가 아닌 언어 버전 설치
description: 영어가 아닌 언어 버전의 SSMS(SQL Server Management Studio) 설치
ms.prod: sql
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 04/25/2019
ms.openlocfilehash: cc4d98322f0422053402bdf097674c90807e11a1
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75246880"
---
# <a name="install-non-english-language-versions-of-sql-server-management-studio-ssms"></a>영어가 아닌 언어 버전의 SSMS(SQL Server Management Studio) 설치

SSMS는 여러 언어로 사용할 수 있지만 시스템 로캘이 SSMS 언어와 일치하지 않을 경우 SSMS 설치 관리자는 컴퓨터에서 설치를 차단합니다.

> [!NOTE]
> 이 문서는 SSMS 17.x에 적용됩니다. SSMS 18.x의 경우 혼합된 언어 설치의 차단이 제거되었으므로 예를 들어 이제 프랑스어 버전의 Windows에 SSMS 독일어를 설치할 수 있습니다. OS 언어가 SSMS 언어와 일치하지 않는 경우 **도구** > **옵션** > **국가별 설정**에서 원하는 언어를 설정합니다. 그렇지 않으면 SSMS에 영어 UI가 표시됩니다.

다음 지침은 Windows 버전에 따라 다릅니다. 다음은 Windows 10용 지침입니다.

## <a name="install-non-english-ssms-on-a-computer-running-an-english-operating-system-os"></a>영어 OS(운영 체제)를 실행 중인 컴퓨터에 영어가 아닌 SSMS 설치

1. SSMS를 사용할 언어의 Windows 언어 팩을 설치합니다.
   - **설정** > **시간 및 언어** > **지역 및 언어** > **언어 추가**
2. 방금 설치한 언어를 클릭하여 이전 단계에서 설치한 언어 팩을 사용하도록 시스템 로캘을 설정한 다음, **기본값으로 설정**을 선택합니다. (SSMS를 설치한 후 시스템 로캘을 다시 영어로 설정할 수 있습니다. )
3. 운영 체제가 원하는 언어로 실행되면 원하는 SSMS 언어를 설치합니다. 새 SSMS 언어를 처음으로 설치할 때는 전체 패키지를 사용합니다. 이후 설치에서는 업그레이드 패키지를 사용할 수 있습니다.
4. SSMS를 실행하면 이전 단계에서 설치한 언어로 표시됩니다.
5. 컴퓨터의 시스템 로캘을 다시 영어로 설정합니다.

## <a name="install-ssms-in-a-language-other-than-the-language-of-the-installed-os"></a>설치된 OS 언어와 다른 언어로 SSMS 설치

1. SSMS를 사용할 언어의 Windows 언어 팩을 설치합니다.
   - **설정** > **시간 및 언어** > **지역 및 언어** > **언어 추가**
2. 방금 설치한 언어를 클릭하여 이전 단계에서 설치한 언어 팩을 사용하도록 시스템 로캘을 설정한 다음, **기본값으로 설정**을 선택합니다.
3. 운영 체제가 원하는 언어로 실행되면 원하는 SSMS 언어를 설치합니다. 새 SSMS 언어를 처음으로 설치할 때는 전체 패키지를 사용합니다. 이후 설치에서는 업그레이드 패키지를 사용할 수 있습니다.
4. 처음 설치한 SSMS 버전의 언어와 일치하지 않는 언어 버전을 설치할 때마다, 해당하는 Visual Studio 2015 Shell(격리) 언어 팩을 설치합니다.
   - [https://connect.microsoft.com/VisualStudio/ExtendVS](https://connect.microsoft.com/VisualStudio/ExtendVS)(*등록 연결* 프로세스에 로그인하여 완료해야 할 수도 있음)로 이동하세요.
   - 원하는 Visual Studio 2015 Shell(격리) 언어 팩을 다운로드하여 설치합니다.

   > [!IMPORTANT]
   > 이전 단계에 따라 Visual Studio 2015 Shell(격리) 언어 팩을 설치하세요. **도구** | **옵션** | **국가별 설정**의 **추가 언어 가져오기** 링크를 사용하지 마세요.

5. SSMS를 실행하고 다음에서 사용할 언어를 선택합니다.
   - **도구** | **옵션** | **국가별 설정**
6. SSMS를 닫고 다시 시작합니다.

## <a name="next-steps"></a>다음 단계

- [자습서: SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/tutorials/tutorial-sql-server-management-studio)
