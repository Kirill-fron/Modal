<template>
    <div class="modal-overlay">
      <div class="modal">
        <button class="close-button" @click="$emit('closeModal')">X</button>
        <div class="modal-content">
          <slot></slot>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ModalComponent'
  };
  </script>
  
  <style>
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .modal {
    background: white;
    padding: 20px;
    margin-top: 50px;
    border-radius: 8px;
    position: relative;
  }
  .close-button {
    position: absolute;
    top: 10px;
    right: 10px;
    background: transparent;
    border: none;
    font-size: 20px;
    cursor: pointer;
  }
  </style>
  