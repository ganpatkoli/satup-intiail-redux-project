1) install  package ,  npm install @reduxjs/toolkit , npm install react-redux

2) create slice  - 


import { createSlice, createAsyncThunk } from "@reduxjs/toolkit";

export const GET_HELPS = createAsyncThunk("user/all/helps", async (data) => {
    const { user_id, token } = data
    console.log(data);
    try {
        const res = await GET_HELP_REQUEST({ _id: user_id }, token);
        return await res;
    } catch (err) {
        return err;
    }
});

const AdminHelpSlice = createSlice({
    name: "AdminHelpSlice",
    initialState: {
        isLoading: false,
        isError: false,
        helps: [],
        status: false
    },

    recuders: {},
    extraReducers: {

        [GET_HELPS.pending]: (state, { payload }) => {
            // state.isLoading = false;
            // return { ...state, get_dashboard: [], isLoading: true };
        },
        [GET_HELPS.fulfilled]: (state, { payload }) => {
            // state.isLoading = false;
            return { ...state, helps: payload, isLoading: false };
        },
        [GET_HELPS.rejected]: (state, action) => {
            // return { ...state, get_dashboard: action, isLoading: false };
        },

    },
});




export default AdminHelpSlice;




3 ) create store 

import { configureStore } from "@reduxjs/toolkit";

//AUTH SLICE
import AuthSlice from "../Slice/Auth/AuthSlice";



const store = configureStore({
  reducer: {
    AuthSlice: AuthSlice.reducer,
    
  },
});

export default store;



4) export store to globally 

import React from "react";
import { HashRouter } from "react-router-dom";
import { Provider } from 'react-redux'
import Store from "./ReduxStore/Store/Store";
const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(
  <>
    <HashRouter>
      <Provider store={Store}>
        <App />
      </Provider>
    </HashRouter>
  </>
);





