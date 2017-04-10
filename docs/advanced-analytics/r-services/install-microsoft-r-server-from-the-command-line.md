---
title: "명령줄에서 Microsoft R Server 설치 | Microsoft Docs"
ms.custom: ""
ms.date: "01/19/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: 4
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 3
---
# 명령줄에서 Microsoft R Server 설치
    
명령줄에서 SQL Server 설치 프로그램과 함께 제공되는 스크립팅 기능을 사용하여 Microsoft R Server를 설치할 수 있습니다. 

- **무인** 설치에서는 설치 유틸리티의 위치를 지정하고 인수를 사용하여 설치할 기능을 나타내야 합니다. 
- **자동** 설치의 경우 동일한 인수를 제공하고 **/q** 스위치를 추가합니다. 프롬프트가 제공되지 않으며 상호 작용도 필요하지 않습니다. 그러나 필수 인수를 생략하면 설치가 실패합니다.

자세한 내용은 [명령 프롬프트에서 SQL Server 2016 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)를 참조하세요.

## <a name="perform-a-command-line-install-of-microsoft-r-server-standalone"></a>Microsoft R Server(독립 실행형)의 명령줄 설치 수행

 다음 예제에서는 SQL Server 설치 프로그램을 사용하여 Microsoft R Server의 명령줄 설치를 수행할 때 사용되는 인수를 보여 줍니다.


### <a name="example-of-unattended-installation-of-r-server-standalone"></a>R Server 독립 실행형의 무인 설치 예

Microsoft R Server(독립 실행형)와 해당 필수 조건만 설치하려면 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다. 

```  
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS 
```  

진행률 및 프롬프트를 보려면 /q 인수를 제거합니다.

다음 인수가 모두 필요합니다.
  - **FEATURES = SQL_SHARED_MR** Microsoft R Open 및 모든 필수 조건을 포함하여 Microsoft R Server 구성 요소만 가져옵니다.
  - **IACCEPTROPENLICENSETERMS** 오픈 소스 R 구성 요소의 사용 약관에 동의했음을 나타냅니다.
  - **IACCEPTSQLSERVERLICENSETERMS** 설치 마법사를 실행하는 데 필요합니다.


### <a name="offline-installation"></a>오프라인 설치

인터넷에 연결되어 있지 않은 컴퓨터에 Microsoft R Server(독립 실행형)를 설치하는 경우 필요한 R 구성 요소를 미리 다운로드하여 로컬 폴더에 복사해야 합니다. 다운로드 위치는 [인터넷에 연결하지 않고 R 구성 요소 설치](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)를 참조하세요.   


## <a name="advanced-installation-tips"></a>고급 설치 팁

설치가 완료되면 설치 작업에 대한 요약 정보와 함께 SQL Server 설치 프로그램에서 만든 구성 파일을 검토할 수 있습니다.

기본적으로 SQL Server 및 관련 기능에 대한 모든 설치 로그 및 요약은 `C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log`에 생성됩니다.

설치된 각 기능에 대해 별도의 하위 폴더가 생성됩니다. Microsoft R Server의 경우 다음을 찾습니다. 
- `RSetup.log`
- `Settings.xml`
- `Summmary<instance_GUID>.txt`

동일한 매개 변수를 사용하여 Microsoft R Server의 다른 인스턴스를 설치하려면 설치 중에 생성된 구성 파일을 다시 사용할 수도 있습니다. 자세한 내용은 [구성 파일을 사용하여 SQL Server 설치](https://msdn.microsoft.com/library/dd239405.aspx)를 참조하세요.



### <a name="customizing-your-r-environment"></a>R 환경 사용자 지정

설치 후 추가 R 패키지를 설치할 수 있습니다. 자세한 내용은 [R 패키지 설치 및 관리](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)를 참조하세요.

> [!IMPORTANT]
> SQL Server에서 R 코드를 실행하려면 Microsoft R Server를 실행하는 클라이언트 컴퓨터와 R Services가 실행되는 SQL Server 인스턴스 둘 다에 동일한 패키지를 설치합니다. 



## <a name="see-also"></a>관련 항목:  

[Microsoft R Server](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)
  