<template>
  <router-view/>
</template>

<style lang="scss">
/* eslint-disable */
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

$green:#28a745;

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Roboto', sans-serif;
}
body {
  background-color: #030e1b;
  color: #FFF;
}
a {
  color: #2aeb74;
  text-decoration: none;
}

.btn {
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: 0.25rem;
  transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
  border:none;
  outline: none;
  background: $green;
  color: #fff;
  cursor: pointer;
  &:hover {
    background: lighten($green,10%);
  }
  &:active {
    background: darken($green,10%);
  }

  &.btn-primary {
    background: #007bff;
    &:hover {
      background: lighten(#007bff, 10%);
    }
    &:active {
      background: darken(#007bff, 10%);
    }
  }
  &.btn-secondary {
    background: #6c757d;
    &:hover {
      background: lighten(#6c757d, 10%);
    }
    &:active {
      background: darken(#6c757d, 10%);
    }
  }
  &.btn-danger {
    background: #dc3545;
    &:hover {
      background: lighten(#dc3545, 10%);
    }
    &:active {
      background: darken(#dc3545, 10%);
    }
  }
  &.btn-warning {
    color: #212529;
    background: #ffc107;
    &:hover {
      background: lighten(#ffc107, 10%);
    }
    &:active {
      background: darken(#ffc107, 10%);
    }
  }
  &.btn-info {
    background: #17a2b8;
    &:hover {
      background: lighten(#17a2b8, 10%);
    }
    &:active {
      background: darken(#17a2b8, 10%);
    }
  }

  &.btn-lg {
    padding: 0.5rem 1rem;
    font-size: 1.25rem;
    line-height: 1.5;
    border-radius: 0.3rem;
  }
}



//button {
//  appearance: none;
//  border: none;
//  cursor: pointer;
//  background: $green;
//  font-size: 1rem;
//  color: #fff;
//  padding: .375rem .75rem;
//  border-radius: 0.3rem;
//  &:hover {
//    background: lighten($green,10%);
//  }
//  &:active {
//    background: darken($green,10%);
//  }
//}
</style>
