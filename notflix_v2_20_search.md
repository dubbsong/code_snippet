###### 코드 추가

- SearchPresenter.js

```react
import React from 'react';
import PropTypes from 'prop-types';
import styled from 'styled-components';

const Container = styled.div`
  margin: 70px 0 50px 0;
  padding: 0 4%;
`;

const Form = styled.form``;

const Input = styled.input`
  all: unset;
  width: 150px;
  font-size: 20px;
  border-bottom: 2px solid #b3b3b3;
`;

const SearchPresenter = ({
  loading,
  searchWord,
  movieResults,
  tvResults,
  error,
  handleSubmit
}) => (
  <Container>
    <Form>
      <Input value={searchWord} placeholder="Search By Word..." />
    </Form>
  </Container>
);

...
```

