# MUI Custom Theme (SHOULD)

MUI 커스텀 테마 설정 규칙

## 테마 파일 관리

- 커스텀 테마는 별도의 파일로 관리한다
- 위치: `src/styles/theme.js` 또는 유사 경로

## Typography

### 본문
- **Pretendard Variable** 버전을 웹폰트로 사용

### Headline
- **영어**: Google Font의 **Outfit**
- **한글**: Pretendard의 가장 높은 weight

## Color

### Primary Color
```jsx
primary: {
  main: '#0000FF'
}
```

### Secondary Color
```jsx
secondary: {
  main: blueGrey[900]  // blueGrey의 가장 어두운색
}
```

## Elevation

Paper에 기본적으로 사용되는 elevation의 box shadow 설정:

- x, y offset: 0
- opacity 값: 낮춤
- blur 값: 높임 (dimmed shadow)

```jsx
shadows: [
  'none',
  '0 0 8px rgba(0, 0, 0, 0.08)',
  '0 0 16px rgba(0, 0, 0, 0.08)',
  // ...
]
```

## Border Radius

인라인으로 직접 지정하지 않는 이상 모든 컴포넌트의 borderRadius는 **0**

```jsx
shape: {
  borderRadius: 0
}
```

## 테마 적용 예시

```jsx
import { createTheme, ThemeProvider } from '@mui/material/styles';

const theme = createTheme({
  palette: {
    primary: { main: '#0000FF' },
    secondary: { main: '#263238' },  // blueGrey[900]
  },
  typography: {
    fontFamily: 'Pretendard Variable, sans-serif',
    h1: {
      fontFamily: 'Outfit, Pretendard Variable, sans-serif',
      fontWeight: 900,
    },
    // ...
  },
  shape: {
    borderRadius: 0,
  },
});

function App() {
  return (
    <ThemeProvider theme={theme}>
      {/* 앱 내용 */}
    </ThemeProvider>
  );
}
```
