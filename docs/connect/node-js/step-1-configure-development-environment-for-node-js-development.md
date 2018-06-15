---
title: '1 단계: Node.js 개발을 위한 개발 환경 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f918eead7fb0af9d28cd85b173e3e076c5ba9416
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35288962"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>1 단계: Node.js 개발을 위한 개발 환경 구성
Node.js 드라이버를 사용 하 여 SQL Server에 대 한 응용 프로그램을 개발 하기 위해 필수 구성 요소 개발 환경을 구성 해야 합니다.  가장 일반적인 방법은 번거로운 모듈을 설치 하는 노드 패키지 관리자 (npm)를 사용 하는 것에 직접 번거로운 모듈을 다운로드할 수 있습니다 하지만 [Github](https://github.com/pekim/tedious) 하려는 경우.  
  
Node.js 드라이버에서는 SQL Server 및 Azure SQL 데이터베이스에 기본적으로 사용 되는 TDS 프로토콜을 참고 합니다.  추가적인 서버 구성은 필요하지 않습니다.  
  
## <a name="windows"></a>Windows  
  
1. **Node.js 런타임 및 npm 패키지 관리자를 설치 합니다.**  
1. 로 이동 [Node.js](https://nodejs.org/en/download/)  
2. 적절 한 Windows installer msi 링크를 클릭 합니다.   
c. 를 다운로드 한 후 실행 Node.js를 설치 하는 msi  
  
2. **Cmd.exe를 엽니다.**  
  
3. **프로젝트 디렉터리를 만들** 것으로 이동 합니다.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **노드 프로젝트를 만듭니다.**  프로젝트를 만드는 동안 기본값을 유지 하려면 프로젝트를 만들 때까지 enter 키를 누릅니다. 이 단계의 끝 package.json 파일을 프로젝트 디렉터리에 표시 됩니다.  
```  
> npm init  
```  
  
5. **프로젝트의 번거로운 모듈을 설치 합니다.**  드라이버를 사용 하 여 SQL Server와 통신 하는 TDS 프로토콜의 구현입니다.  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **열기 터미널**  
  
2. **Node.js 런타임을 설치합니다**  
```  
>sudo apt-get install node  
```  
3. **Npm (노드 패키지 관리자)를 설치 합니다.**  
```  
> sudo apt-get install npm  
```  
4. **프로젝트 디렉터리를 만들** 것으로 이동 합니다.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **노드 프로젝트를 만듭니다.**  프로젝트를 만드는 동안 기본값을 유지 하려면 프로젝트를 만들 때까지 enter 키를 누릅니다. 이 단계의 끝 package.json 파일을 프로젝트 디렉터리에 표시 됩니다.  
```  
> sudo npm init  
```  
  
6. **프로젝트의 번거로운 모듈을 설치 합니다.**  드라이버를 사용 하 여 SQL Server와 통신 하는 TDS 프로토콜의 구현입니다.  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **Node.js 런타임 및 npm 패키지 관리자를 설치 합니다.**  
1. 로 이동 [Node.js](https://nodejs.org/en/download/)  
2. 적절 한 Mac 운영 체제 설치 관리자 링크를 클릭 합니다.  
c. 를 다운로드 한 후 실행 dmg Node.js를 설치 하려면  
  
2. **열기 터미널**  
  
3. **프로젝트 디렉터리를 만들** 것으로 이동 합니다.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **노드 프로젝트를 만듭니다.**  프로젝트를 만드는 동안 기본값을 유지 하려면 프로젝트를 만들 때까지 enter 키를 누릅니다. 이 단계의 끝 package.json 파일을 프로젝트 디렉터리에 표시 됩니다.  
```  
> npm init  
```  
  
5. **프로젝트의 번거로운 모듈을 설치 합니다.**  드라이버를 사용 하 여 SQL Server와 통신 하는 TDS 프로토콜의 구현입니다.  
```  
> npm install tedious  
```  
  
