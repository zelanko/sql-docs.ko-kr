---
title: '1단계: Node.js 개발을 위한 개발 환경 구성 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ba06f87c5ff4970d3d8686e7195d57dc076cc04
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923834"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>1단계: Node.js 개발을 위한 개발 환경 구성
SQL Server의 Node.js 드라이버로 애플리케이션을 개발하려면 개발 환경을 필수 구성 요소로 구성해야 합니다.  가장 일반적인 방법은 npm(노드 패키지 관리자)으로 Tedious 모듈을 설치하는 것이지만, 원한다면 [Github](https://github.com/pekim/tedious)에서 Tedious 모듈을 직접 다운로드할 수도 있습니다.  
  
Node.js 드라이버는 SQL Server와 Azure SQL Database에서 기본적으로 사용 설정되는 TDS 프로토콜을 사용합니다.  추가적인 서버 구성은 필요하지 않습니다.  
  
## <a name="windows"></a>Windows  
  
1. **Node.js 런타임 및 npm 패키지 관리자를 설치합니다.**  
a. [Node.js](https://nodejs.org/en/download/)로 이동합니다.  
b. 적절한 Windows Installer msi 링크를 클릭합니다.   
다. 다운로드가 완료되면 msi를 실행하여 Node.js를 설치합니다.  
  
2. **cmd.exe를 엽니다.**  
  
3. **프로젝트 디렉터리를 만들고** 해당 디렉터리로 이동합니다.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **노드 프로젝트를 만듭니다.**  프로젝트를 만드는 동안 기본값을 유지하려면 프로젝트가 만들어질 때까지 Enter 키를 누릅니다. 이 단계가 끝나면 프로젝트 디렉터리에 package.json 파일이 표시됩니다.  
```  
> npm init  
```  
  
5. **프로젝트에 Tedious 모듈을 설치합니다.**  그러면 드라이버가 SQL Server와의 통신에 사용하는 TDS 프로토콜이 구현됩니다.  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **터미널을 엽니다.**  
  
2. **Node.js 런타임을 설치합니다.**  
```  
>sudo apt-get install node  
```  
3. **npm(노드 패키지 관리자)을 설치합니다.**  
```  
> sudo apt-get install npm  
```  
4. **프로젝트 디렉터리를 만들고** 해당 디렉터리로 이동합니다.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **노드 프로젝트를 만듭니다.**  프로젝트를 만드는 동안 기본값을 유지하려면 프로젝트가 만들어질 때까지 Enter 키를 누릅니다. 이 단계가 끝나면 프로젝트 디렉터리에 package.json 파일이 표시됩니다.  
```  
> sudo npm init  
```  
  
6. **프로젝트에 Tedious 모듈을 설치합니다.**  그러면 드라이버가 SQL Server와의 통신에 사용하는 TDS 프로토콜이 구현됩니다.  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **Node.js 런타임 및 npm 패키지 관리자를 설치합니다.**  
a. [Node.js](https://nodejs.org/en/download/)로 이동합니다.  
b. 적절한 Mac OS 설치 관리자 링크를 클릭합니다.  
다. 다운로드가 완료되면 dmg를 실행하여 Node.js를 설치합니다  
  
2. **터미널을 엽니다.**  
  
3. **프로젝트 디렉터리를 만들고** 해당 디렉터리로 이동합니다.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **노드 프로젝트를 만듭니다.**  프로젝트를 만드는 동안 기본값을 유지하려면 프로젝트가 만들어질 때까지 Enter 키를 누릅니다. 이 단계가 끝나면 프로젝트 디렉터리에 package.json 파일이 표시됩니다.  
```  
> npm init  
```  
  
5. **프로젝트에 Tedious 모듈을 설치합니다.**  그러면 드라이버가 SQL Server와의 통신에 사용하는 TDS 프로토콜이 구현됩니다.  
```  
> npm install tedious  
```  
  
