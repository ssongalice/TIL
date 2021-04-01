# Atomic Design Pattern

## Atomic Design Pattern?

- 디자인 요소를 나눠서 파악하고 요소를 조합해 디자인을 구성
- 리액트는 컴포넌트를 중심으로 만들어지는 프레임워크로 컴포넌트의 재사용성이 매우 중요.
- 개발 단계부터 재사용성이 용이하고 여러 컴포넌트들을 모아 또 다른 컴포넌트를 만들 수 있도록 고민하며 개발하는 것이 중요해짐.
- 아토믹 디자인은 Atom, Molecule, Orgamisn, Template, Page로 나눌 수 있다.

## Atom?

- 각 요소를 이루는 가장 작은 단위의 컴포넌트. 기능/의미론적으로 가장 작은 단위
- 앞으로 계속 재활용하기 때문에 특정 기능을 수행하는 것이 아니라 일반적으로 사용할 수 있도록 구현.
- 함수나 기능을 props로 전달받아 사용할 수 있도록 구현.
- 아톰은 마진이나 위치값을 가지고 있지 않는다
- 예시 : label, input, button

## Molecule

- Atom들을 엮은 하나의 기능을 하는 블럭 단위
- 예시: FormInput = Label + Input + Button

## Organism

- Molecule들의 집합.
- 독립적, 재사용이 가능한 컴포넌트들의 구성
- Organism에서 값을 들고 하위 Molecule 또는 Atom으로 전달
- Organism에서 Atom과 Molecule의 위치값을 조정함
- 예시: SignUpForm = 4 FormInputs

## Template

- 템플릿은 오로지 레이아웃만 정함. Organism과 component의 위치값만 지정
- 레이아웃을 그려주고 안에 컴포넌트를 채우면 Page가 된다.

## Page

- 템플릿을 이용해 각 그리드에 컴포넌트를 포함한 결과물
