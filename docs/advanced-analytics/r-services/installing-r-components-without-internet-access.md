---
title: "인터넷에 액세스하지 않고 R 구성 요소 설치 | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: 30
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 21
---
# 인터넷에 액세스하지 않고 R 구성 요소 설치
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 사용하는 R 구성 요소를 설치하려면 Microsoft 다운로드 센터 또는 기타 신뢰할 수 있는 사이트에서 제공되는 파일에 액세스하기 위해 인터넷에 연결해야 합니다. 그러나 이 항목의 설명에 따라 로컬 복사본을 만들면 인터넷에 액세스하지 않고 서버에 이러한 구성 요소를 설치할 수 있습니다.  
  
  > [!TIP]
  > 
  > 오프라인 설치 프로세스의 자세한 연습은 [SQL Server 고객 자문 팀](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/do-it-right-deploying-sql-server-r-services-on-computers-without-internet-access/)에서 제공하는 이 블로그를 참조하세요.
  
## <a name="installation-on-computers-with-no-internet-access"></a>인터넷에 액세스할 수 없는 컴퓨터에 구성 요소 설치  
 오프라인 설치를 수행하는 경우 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 필요한 R 구성 요소 설치를 위한 링크에 액세스할 수 없습니다. 이 문제를 방지하려면 설치 관리자 복사본을 로컬에 다운로드하고 여기에 설명된 대로 설치를 완료할 수 있습니다.
 
 Microsoft R Open과 Microsoft R Server에 대해 각각 하나씩, 두 개의 R 구성 요소 설치 관리자가 있습니다. SQL Server R Services를 사용하려면 둘 다 다운로드해서 설치해야 합니다. SQL Server 설치 마법사는 설치 관리자가 올바른 순서로 설치되도록 합니다.


릴리스  |다운로드 링크  
---------|---------
**SQL Server 2016 RTM**     |           
Microsoft R Open     |[SRO_3.2.2.803_1033.cab](https://go.microsoft.com/fwlink/?LinkId=761266)     
Microsoft R Server     |[SRS_8.0.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=735051)      
**SQL Server 2016 CU 1**     |           
Microsoft R Open     |[SRO_3.2.2.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808803)     
Microsoft R Server     |[SRS_8.0.3.10000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=808805)      
**SQL Server 2016 CU 2**     |           
Microsoft R Open     |[SRO_3.2.2.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827398)     
Microsoft R Server     |[SRS_8.0.3.12000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=827399)  
**SQL Server 2016 CU 3**     |           
Microsoft R Open     |[SRO_3.2.2.13000_1033.cab: ](https://go.microsoft.com/fwlink/?LinkId=831785)     
Microsoft R Server     |[SRS_8.0.3.13000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=831676)  |
**SQL Server 2016 SP 1**     |           
Microsoft R Open     |[SRO_3.2.2.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824879)     
Microsoft R Server     |[SRS_8.0.3.15000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=824881)  
**SQL Server 2016 SP 1 GDR**     |           
Microsoft R Open     |[SRO_3.2.2.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836819)     
Microsoft R Server     |[SRS_8.0.3.16000_1033.cab](https://go.microsoft.com/fwlink/?LinkId=836818)  

  
**오프라인 설치에서 R 구성 요소를 업데이트하는 방법**     

1. 위에 나열된 링크를 사용하여 적절한 버전을 다운로드합니다.
2. 업데이트를 설치할 컴퓨터의 폴더에 CAB 파일을 복사합니다.
3. SQL Server 설치 마법사를 실행하는 경우 Microsoft R 라이선스 페이지에서 **동의**를 클릭합니다.  다운로드 링크가 나열된 대화 상자가 나타납니다. 다운로드한 파일 위치의 경로를 입력합니다. 
4. **다음**을 클릭하여 구성 요소를 사용할 수 있다고 지정하고 SQL Server 설치 마법사를 완료합니다.
5. 필요에 따라 오픈 소스 구성 요소에 대한 보관된 소스 코드를 다운로드할 수도 있습니다. 자세한 내용은 [SQL Server R Services 설정](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)을 참조하세요.


> [!IMPORTANT] 인터넷에 연결된 컴퓨터에서 SQL Server 설치의 일부로 .cab 파일을 다운로드하는 경우 설치 마법사에서 로컬 언어를 검색하고 설치 관리자의 언어를 자동으로 변경합니다. 
> 
> 그러나 인터넷에 연결되지 않은 컴퓨터에 지역화된 버전의 SQL Server 중 하나를 설치 중이며 R 설치 관리자를 로컬 공유로 다운로드하는 경우에는 다운로드한 파일의 이름을 수동으로 편집하고 설치 중인 언어에 맞는 올바른 언어 식별자를 삽입해야 합니다. 
> 
> 예를 들어 일본어 버전의 SQL Server를 설치하는 경우 파일 이름을 SRS_8.0.3.0_1033.cab에서 SRS_8.0.3.0_1041.cab로 변경합니다.    
 
  
## <a name="see-also"></a>관련 항목:  
 [SQL Server R Services 시작](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 [R Services 설치 문제 해결](../Topic/Troubleshooting%20R%20Services%20Setup.md)  
  
  