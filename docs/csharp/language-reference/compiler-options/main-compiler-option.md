---
title: -main(C# 컴파일러 옵션)
ms.date: 07/20/2015
f1_keywords:
- /main
helpviewer_keywords:
- -main compiler option [C#]
- main compiler option [C#]
- /main compiler option [C#]
ms.assetid: 975cf4d5-36ac-4530-826c-4aad0c7f2049
ms.openlocfilehash: 7d3cfce474023907eda0bc40b692e4bbb65ffb96
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/22/2020
ms.locfileid: "83802838"
---
# <a name="-main-c-compiler-options"></a>-main(C# 컴파일러 옵션)
이 옵션은 둘 이상의 클래스에 **Main** 메서드가 포함된 경우 프로그램에 대한 진입점을 포함하는 클래스를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```console  
-main:class  
```  
  
## <a name="arguments"></a>인수  
 `class`  
 **Main** 메서드를 포함하는 형식입니다.  
 제공된 클래스 이름은 완전히 정규화되어야 하며, 클래스를 포함하는 전체 네임스페이스와 클래스 이름을 포함해야 합니다. 예를 들어 `Main` 메서드가 `MyApplication.Core` 네임스페이스의 `Program` 클래스 내에 있는 경우 컴파일러 옵션은 `-main:MyApplication.Core.Program`이어야 합니다.
  
## <a name="remarks"></a>설명  
 컴파일에 [Main](../../programming-guide/main-and-command-args/index.md) 메서드가 있는 형식이 둘 이상 포함된 경우 프로그램에 대한 진입점으로 사용할 **Main** 메서드를 포함하는 형식을 지정할 수 있습니다.  
  
 이 옵션은 .exe 파일을 컴파일할 때 사용됩니다.  
  
### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>Visual Studio 개발 환경에서 이 컴파일러 옵션을 설정하려면  
  
1. 프로젝트 **속성** 페이지를 엽니다.  
  
2. **애플리케이션** 속성 페이지를 클릭합니다.  
  
3. **시작 개체** 속성을 수정합니다.  
  
     프로그래밍 방식으로 이 컴파일러 옵션을 설정하려면 <xref:VSLangProj80.ProjectProperties3.StartupObject%2A>를 참조하세요.  
  
### <a name="to-set-this-compiler-option-by-manually-editing-the-csproj-file"></a>수동으로 .csproj 파일을 편집하여 이 컴파일러 옵션을 설정하려면
  
.csproj 파일을 편집하고 `PropertyGroup` 섹션 내에 `StartupObject` 요소를 추가하여 이 옵션을 설정할 수 있습니다. 예를 들어:

```
  <PropertyGroup>
    ...
    <StartupObject>MyApplication.Core.Program</StartupObject>
  </PropertyGroup>
```

## <a name="example"></a>예제  
 **Main** 메서드가 `Test2`에 있다고 지정하여 `t2.cs` 및 `t3.cs`를 컴파일합니다.  
  
```console  
csc t2.cs t3.cs -main:Test2  
```  
  
## <a name="see-also"></a>참조

- [C# 컴파일러 옵션](./index.md)
- [프로젝트 및 솔루션 속성 관리](/visualstudio/ide/managing-project-and-solution-properties)
