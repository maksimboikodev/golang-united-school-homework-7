package coverage

import (
	"fmt"
	"os"
	"testing"
	"time"
	"github.com/stretchr/testify/assert"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW

func TestLen(t *testing.T) {
	testCases := []struct {
		name  string
		input People
	}{
		{
			name:  "Length is nil",
			input: nil,
		},
		{
			name:  "Length is 0",
			input: make(People, 0),
		},
		{
			name:  "Length is 100",
			input: make(People, 100),
		},
	}

	for _, testCase := range testCases {
		t.Run(testCase.name, func(t *testing.T) {
			if len(testCase.input) != testCase.input.Len() {
				t.Errorf("got: %v, want: %v", testCase.input.Len(), len(testCase.input))
			}
		})
	}
}

func TestLess(t *testing.T) {
	people := People{
		Person{firstName: "A", lastName: "B", birthDay: time.Date(2000, 1, 1, 0, 0, 0, 0, time.UTC)},
		Person{firstName: "B", lastName: "Z", birthDay: time.Date(2000, 2, 1, 0, 0, 0, 0, time.UTC)},
		Person{firstName: "G", lastName: "D", birthDay: time.Date(2000, 1, 1, 0, 0, 0, 0, time.UTC)},
		Person{firstName: "G", lastName: "E", birthDay: time.Date(2000, 1, 1, 0, 0, 0, 0, time.UTC)},
	};

	testCases := []struct {
		name  string
		input People
		i int
		j int
		want bool
	}{
		{
			name:  "Person is less by birthday",
			input: people,
			i: 1,
			j: 0,
			want: true,
		},
		{
			name:  "Person is not less by birthday",
			input: people,
			i: 0,
			j: 1,
			want: false,
		},
		{
			name:  "Person is less by firstname",
			input: people,
			i: 0,
			j: 2,
			want: true,
		},
		{
			name:  "Person is not less by firstname",
			input: people,
			i: 2,
			j: 0,
			want: false,
		},
		{
			name:  "Person is less by lastname",
			input: people,
			i: 2,
			j: 3,
			want: true,
		},
		{
			name:  "Person is not less by lastname",
			input: people,
			i: 3,
			j: 2,
			want: false,
		},
	}

	for _, testCase := range testCases {
		t.Run(testCase.name, func(t *testing.T) {
			if testCase.want != testCase.input.Less(testCase.i, testCase.j) {
				t.Errorf("got: %v, want: %v", testCase.input.Less(testCase.i, testCase.j), testCase.want)
			}
		})
	}
}

func TestSwap(t *testing.T) {
	people := People{
		Person{firstName: "A", lastName: "B", birthDay: time.Date(2000, 1, 1, 0, 0, 0, 0, time.UTC)},
		Person{firstName: "B", lastName: "Z", birthDay: time.Date(2000, 2, 1, 0, 0, 0, 0, time.UTC)},
	};

	testCases := []struct {
		name  string
		input People
		i int
		j int
		want Person
	}{
		{
			name:  "Person B must be first",
			input: people,
			i: 0,
			j: 1,
			want: Person{firstName: "B", lastName: "Z", birthDay: time.Date(2000, 2, 1, 0, 0, 0, 0, time.UTC)},
		},
		{
			name:  "Person A must be first",
			input: people,
			i: 0,
			j: 1,
			want: Person{firstName: "A", lastName: "B", birthDay: time.Date(2000, 1, 1, 0, 0, 0, 0, time.UTC)},
		},
	}

	for _, testCase := range testCases {
		t.Run(testCase.name, func(t *testing.T) {
			testCase.input.Swap(testCase.i, testCase.j)

			if testCase.want != people[0] {
				t.Errorf("got: %v, want: %v", testCase.input.Less(testCase.i, testCase.j), testCase.want)
			}
		})
	}
}

func TestNew(t *testing.T) {
	testCases := []struct {
		name  string
		input string
		want *Matrix
		err error
	}{
		{
			name:  "Empty string",
			input: "",
			want: nil,
			err: fmt.Errorf("strconv.Atoi: parsing \"\": invalid syntax"),
		},
		{
			name:  "Wrong string",
			input: "0 1\n0 1 2",
			want: nil,
			err: fmt.Errorf("Rows need to be the same length"),
		},
		{
			name:  "One row",
			input: "0 1 2 3",
			want: &Matrix{
				rows: 1,
				cols: 4,
				data: []int{0,1,2,3},
			},
			err: nil,
		},
		{
			name:  "Three rows",
			input: "0 1 2\n3 4 5\n6 7 8",
			want: &Matrix{
				rows: 3,
				cols: 3,
				data: []int{0, 1, 2, 3, 4, 5, 6, 7, 8},
			},
			err: nil,
		},
		{
			name:  "Three rows with spaces",
			input: " 0 1 2\n 3 4 5 \n6 7 8 ",
			want: &Matrix{
				rows: 3,
				cols: 3,
				data: []int{0, 1, 2, 3, 4, 5, 6, 7, 8},
			},
			err: nil,
		},
	}

	for _, testCase := range testCases {
		t.Run(testCase.name, func(t *testing.T) {
			actual, err := New(testCase.input)

			assert.Equal(t, testCase.want, actual)

			if err != nil {
				if testCase.err.Error() != err.Error() {
					t.Errorf("Error got: %v, want: %v", err, testCase.err)
				}
			}
		})
	}
}

func TestRows(t *testing.T) {
	testCases := []struct {
		name  string
		input string
		want [][]int
	}{
		{
			name:  "One row",
			input: "0 1 2 3",
			want: [][]int{{0, 1, 2, 3}},
		},
		{
			name:  "Three rows",
			input: "0 1 2\n3 4 5\n6 7 8",
			want: [][]int{{0, 1, 2}, {3, 4, 5}, {6, 7, 8}},
		},
	}

	for _, testCase := range testCases {
		t.Run(testCase.name, func(t *testing.T) {
			actual, _ := New(testCase.input)

			assert.Equal(t, testCase.want, actual.Rows())
		})
	}
}

func TestCols(t *testing.T) {
	testCases := []struct {
		name  string
		input string
		want [][]int
	}{
		{
			name:  "One row",
			input: "0 1 2 3",
			want: [][]int{{0}, {1}, {2}, {3}},
		},
		{
			name:  "Three rows",
			input: "0 1 2\n3 4 5\n6 7 8",
			want: [][]int{{0, 3, 6}, {1, 4, 7}, {2, 5, 8}},
		},
	}


	for _, testCase := range testCases {
		t.Run(testCase.name, func(t *testing.T) {
			actual, _ := New(testCase.input)

			assert.Equal(t, testCase.want, actual.Cols())
		})
	}
}

func TestSet(t *testing.T) {
	testCases := []struct {
		name  string
		input string
		row int
		col int
		value int
		want bool
	}{
		{
			name:  "Row is negative",
			input: "0 1 2 3",
			row: -1,
			col: 0,
			value: 0,
			want: false,
		},
		{
			name:  "Column is negative",
			input: "0 1 2 3",
			row: 0,
			col: -1,
			value: 0,
			want: false,
		},
		{
			name:  "Row is out of range",
			input: "0 1 2 3",
			row: 1,
			col: 0,
			value: 0,
			want: false,
		},
		{
			name:  "Column is out of range",
			input: "0 1 2 3",
			row: 0,
			col: 4,
			value: 0,
			want: false,
		},
		{
			name:  "One row",
			input: "0 1 2 3",
			row: 0,
			col: 1,
			value: 4,
			want: true,
		},
		{
			name:  "Three rows",
			input: "0 1 2\n3 4 5\n6 7 8",
			row: 2,
			col: 2,
			value: 9,
			want: true,
		},
	}

	for _, testCase := range testCases {
		t.Run(testCase.name, func(t *testing.T) {
			actual, _ := New(testCase.input)
			got := actual.Set(testCase.row, testCase.col, testCase.value)

			if testCase.want != got {
				t.Errorf("got: %v, want: %v", got, testCase.want)
			}
		})
	}
}