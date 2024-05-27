```tsx

import {
    ChangeEvent,
    Dispatch,
    FormEvent,
    SetStateAction,
    useState,
} from "react";

type DataStateType = {
    name: string;
    password: string;
};

function App() {

    const [data, setData] = useState<DataStateType>({
        name: "",
        password: "",
    });

    function handleSubmit(e: FormEvent) {
        e.preventDefault();
        console.log(data);
    }

    return (
        <>
            <form onSubmit={handleSubmit}>
                <LabelInput
                    type="text"
                    placeholder="Enter your name"
                    name="name"
                    value={data.name}
                    setData={setData}
                />
                <LabelInput
                    type="password"
                    placeholder="Enter your password"
                    name="password"
                    value={data.password}
                    setData={setData}
                />
                <button type="submit">Submit</button>
            </form>
        </>
    );
}

// Label Component

type LabelInputType = {
    type: string;
    placeholder: string;
    name: string;
    value: string;
    setData: Dispatch<SetStateAction<DataStateType>>;
};

function LabelInput({
    type,
    placeholder,
    name,
    value,
    setData,
}: LabelInputType) {

    function handleChange(e: ChangeEvent<HTMLInputElement>) {
        setData((prev) => {
            return { ...prev, [name]: e.target.value };
        });
        console.log(e.target.value);
    }

    return (
        <div>
            <label>{name} : </label>
            <input
                type={type}
                placeholder={placeholder}
                name={name}
                value={value}
                onChange={handleChange}
            />
        </div>
    );
}

export default App;

```